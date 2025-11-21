<script lang="ts">
	import { onMount, tick } from 'svelte';

	interface Props {
		disabled?: boolean;
		type?: 'button' | 'submit' | 'reset';
		animationSpeed?: 'fast' | 'medium' | 'slow';
		color?: string;
		hoverColor?: string;
		disabledColor?: string;
		fontSize?: string;
		fontWeight?: number | string;
		class?: string;
		[key: string]: unknown;
	}

	let {
		disabled = false,
		type = 'button',
		animationSpeed = 'fast',
		color = '#000000',
		hoverColor = '#666666',
		disabledColor = '#999999',
		fontSize = '2rem',
		fontWeight = 700,
		class: className = '',
		...rest
	}: Props = $props();

	let buttonElement: HTMLButtonElement;
	let hiddenTextElement: HTMLSpanElement;
	let textElement1: HTMLSpanElement;
	let textElement2: HTMLSpanElement;
	let letters: string[] = $state([]);
	
	let translateY = $state(0);
	let isAnimated = $state(false);
	let isAnimating = $state(false);
	let transitionEndCount = $state(0);
	let pendingAction: 'enter' | 'leave' | null = $state(null);
	let animationDirection: 'up' | 'down' | null = $state(null);

	function getSpeedMultiplier(index: number, total: number): number {
		const center = total / 2;
		const distanceFromCenter = Math.abs(index - center);
		const maxDistance = center;
		const normalizedDistance = distanceFromCenter / maxDistance;
		return 0.5 + (1 - normalizedDistance) * 0.25;
	}

	function getDelay(index: number, total: number): number {
		const center = total / 2;
		const distanceFromCenter = Math.abs(index - center);
		return distanceFromCenter * 0.02;
	}

	function calculateTranslate() {
		if (!buttonElement || !hiddenTextElement) return;

		const buttonHeight = buttonElement.offsetHeight;
		const textHeight = hiddenTextElement.offsetHeight;
		translateY = -(buttonHeight + textHeight + 20);
	}

	function extractAndSplitText() {
		if (hiddenTextElement) {
			const text = hiddenTextElement.textContent || hiddenTextElement.innerText || '';
			const trimmed = text.trim();
			if (trimmed && trimmed.length > 0) {
				letters = trimmed.split('');
				calculateTranslate();
				return true;
			}
		}
		return false;
	}

	async function startAnimationUp() {
		if (disabled) return;
		
		if (letters.length === 0) {
			extractAndSplitText();
			await tick();
		}
		
		if (isAnimating) {
			if (animationDirection === 'down') {
				pendingAction = 'enter';
				return;
			}
			if (animationDirection === 'up' && isAnimated) {
				return;
			}
		}
		
		animationDirection = 'up';
		transitionEndCount = 0;
		
		if (isAnimated) {
			isAnimated = false;
			await tick();
			
			const letter1Elements = buttonElement.querySelectorAll('.letter-1');
			const letter2Elements = buttonElement.querySelectorAll('.letter-2');
			
			letter1Elements.forEach((el) => {
				(el as HTMLElement).style.transition = 'none';
			});
			letter2Elements.forEach((el) => {
				(el as HTMLElement).style.transition = 'none';
			});
			
			buttonElement.offsetHeight;
			
			requestAnimationFrame(() => {
				requestAnimationFrame(() => {
					letter1Elements.forEach((el) => {
						(el as HTMLElement).style.transition = '';
					});
					letter2Elements.forEach((el) => {
						(el as HTMLElement).style.transition = '';
					});
					isAnimating = true;
					isAnimated = true;
				});
			});
		} else {
			isAnimating = true;
			isAnimated = true;
		}
	}

	async function startAnimationDown() {
		if (disabled) return;
		
		if (!isAnimated) {
			pendingAction = 'leave';
			return;
		}
		
		if (isAnimating) {
			if (animationDirection === 'up') {
				pendingAction = 'leave';
				return;
			}
			if (animationDirection === 'down') {
				return;
			}
		}
		
		animationDirection = 'down';
		transitionEndCount = 0;
		isAnimating = true;
		isAnimated = false;
	}

	async function handleMouseEnter() {
		await startAnimationUp();
	}

	async function handleMouseLeave() {
		await startAnimationDown();
	}

	async function handleTransitionEnd(e: TransitionEvent) {
		if (e.propertyName === 'transform' && isAnimating) {
			transitionEndCount++;
			const totalTransitions = letters.length > 0 ? letters.length * 2 : 2;
			if (transitionEndCount >= totalTransitions) {
				isAnimating = false;
				transitionEndCount = 0;
				
				if (animationDirection === 'up' && isAnimated) {
					animationDirection = null;
				} else if (animationDirection === 'down' && !isAnimated) {
					animationDirection = null;
				}
				
				if (pendingAction === 'enter') {
					pendingAction = null;
					await tick();
					await startAnimationUp();
				} else if (pendingAction === 'leave') {
					pendingAction = null;
					await tick();
					await startAnimationDown();
				}
			}
		}
	}

	$effect(() => {
		if (hiddenTextElement && hiddenTextElement.textContent) {
			extractAndSplitText();
		}
	});

	onMount(() => {
		const intervals = [0, 10, 50, 100, 200, 500];
		intervals.forEach(delay => {
			setTimeout(() => {
				extractAndSplitText();
			}, delay);
		});
		
		window.addEventListener('resize', calculateTranslate);
		return () => {
			window.removeEventListener('resize', calculateTranslate);
		};
	});
</script>

<button
	type={type}
	class="simple-button {className}"
	bind:this={buttonElement}
	{disabled}
	style="--button-color: {color}; --button-hover-color: {hoverColor}; --button-disabled-color: {disabledColor}; --button-font-size: {fontSize}; --button-font-weight: {fontWeight};"
	{...rest}
	onmouseenter={handleMouseEnter}
	onmouseleave={handleMouseLeave}
>
	<span 
		bind:this={hiddenTextElement}
		style="position: absolute; opacity: 0; pointer-events: none; white-space: nowrap; visibility: hidden;"
	>
		<slot />
	</span>
	
	<span 
		class="button-text-container button-text-1"
		bind:this={textElement1}
	>
		{#if letters.length > 0}
			{#each letters as letter, index}
				<span
					class="letter letter-1 {isAnimated ? 'animate' : ''} speed-{animationSpeed}"
					style="--translate-y: {translateY}px; --speed-multiplier: {getSpeedMultiplier(index, letters.length)}; --delay: {getDelay(index, letters.length)}s;"
					ontransitionend={handleTransitionEnd}
				>
					{letter === ' ' ? '\u00A0' : letter}
				</span>
			{/each}
		{:else}
			<slot />
		{/if}
	</span>
	
	<span 
		class="button-text-container button-text-2 {isAnimated ? 'animate' : ''} speed-{animationSpeed}"
		bind:this={textElement2}
		style="--translate-y-initial: {-translateY}px;"
		ontransitionend={handleTransitionEnd}
	>
		{#if letters.length > 0}
			{#each letters as letter, index}
				<span
					class="letter letter-2 speed-{animationSpeed}"
					style="--speed-multiplier: {getSpeedMultiplier(index, letters.length)}; --delay: {getDelay(index, letters.length)}s;"
					ontransitionend={handleTransitionEnd}
				>
					{letter === ' ' ? '\u00A0' : letter}
				</span>
			{/each}
		{:else}
			<slot />
		{/if}
	</span>
</button>

<style>
	.simple-button {
		position: relative;
		font-family: 'Mona Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
		font-weight: var(--button-font-weight, 700);
		font-size: var(--button-font-size, 2rem);
		background: none;
		border: none;
		padding: 0;
		margin: 0;
		cursor: pointer;
		color: var(--button-color, #000000);
		outline: none;
		text-transform: uppercase;
		overflow: hidden;
		display: inline-flex;
		align-items: center;
		justify-content: center;
		min-height: 2.5em;
		transition: color 0.2s ease;
	}

	.simple-button:hover:not(:disabled) {
		color: var(--button-hover-color, #666666);
	}

	.simple-button:focus-visible {
		outline: 2px solid var(--button-color, #000000);
		outline-offset: 2px;
	}

	.simple-button:disabled {
		pointer-events: none;
		color: var(--button-disabled-color, #999999);
		opacity: 0.5;
		cursor: not-allowed;
	}

	.button-text-container {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		white-space: nowrap;
		line-height: 1;
	}

	.button-text-container.button-text-1 {
		position: static;
		z-index: 0;
	}

	.button-text-container.button-text-2 {
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		opacity: 0;
		pointer-events: none;
		z-index: 2;
		width: 100%;
		text-align: center;
	}

	.button-text-container.button-text-2.speed-fast {
		transition: opacity 1s cubic-bezier(0.4, 0, 0.2, 1) 0.25s;
	}

	.button-text-container.button-text-2.speed-medium {
		transition: opacity 2s cubic-bezier(0.4, 0, 0.2, 1) 0.5s;
	}

	.button-text-container.button-text-2.speed-slow {
		transition: opacity 3s cubic-bezier(0.4, 0, 0.2, 1) 0.75s;
	}

	.button-text-container.button-text-2.animate {
		opacity: 1 !important;
	}

	.button-text-container.button-text-2:not(.animate) {
		opacity: 0 !important;
	}

	.letter {
		display: inline-block;
		transform: translateY(0);
		line-height: 1;
	}

	.letter-1 {
		transform: translateY(0);
	}

	.letter-1.speed-fast {
		transition: transform calc(1s * var(--speed-multiplier, 1)) cubic-bezier(0.4, 0, 0.2, 1) var(--delay, 0s);
	}

	.letter-1.speed-medium {
		transition: transform calc(2s * var(--speed-multiplier, 1)) cubic-bezier(0.4, 0, 0.2, 1) var(--delay, 0s);
	}

	.letter-1.speed-slow {
		transition: transform calc(3s * var(--speed-multiplier, 1)) cubic-bezier(0.4, 0, 0.2, 1) var(--delay, 0s);
	}

	.letter-1.animate {
		transform: translateY(var(--translate-y, 0px));
	}

	.letter-1:not(.animate) {
		transform: translateY(0);
	}

	.letter-2 {
		transform: translateY(var(--translate-y-initial, 0px));
	}

	.letter-2.speed-fast {
		transition: transform calc(1s * var(--speed-multiplier, 1)) cubic-bezier(0.4, 0, 0.2, 1) var(--delay, 0s);
	}

	.letter-2.speed-medium {
		transition: transform calc(2s * var(--speed-multiplier, 1)) cubic-bezier(0.4, 0, 0.2, 1) var(--delay, 0s);
	}

	.letter-2.speed-slow {
		transition: transform calc(3s * var(--speed-multiplier, 1)) cubic-bezier(0.4, 0, 0.2, 1) var(--delay, 0s);
	}

	.button-text-container.button-text-2.animate .letter-2 {
		transform: translateY(0) !important;
	}

	.button-text-container.button-text-2:not(.animate) .letter-2 {
		transform: translateY(var(--translate-y-initial, 0px)) !important;
	}
</style>
