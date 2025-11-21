<script lang="ts">
	import { onMount, tick } from 'svelte';

	interface Props {
		disabled?: boolean;
		type?: 'button' | 'submit' | 'reset';
		animationSpeed?: 'fast' | 'medium' | 'slow';
		animationType?: 'slide' | 'arc';
		variant?: 'default' | 'default-rounded' | 'outline' | 'outline-rounded' | 'destructive' | 'destructive-rounded' | 'ghost' | 'ghost-rounded';
		class?: string;
		[key: string]: unknown;
	}

	let {
		disabled = false,
		type = 'button',
		animationSpeed = 'fast',
		animationType = 'slide',
		variant = 'default',
		class: className = '',
		...rest
	}: Props = $props();

	const isRounded = variant.includes('-rounded');
	const baseVariant = variant.replace('-rounded', '') as 'default' | 'outline' | 'destructive' | 'ghost';

	const buttonHeight = 4;
	const fontSizeRatio = 0.35;

	let buttonElement: HTMLButtonElement;
	let textElement: HTMLSpanElement;
	let textElement2: HTMLSpanElement;
	
	let translateXText1 = $state(0);
	let translateXText2Initial = $state(0);
	
	let isAnimated = $state(false);
	let isAnimating = $state(false);
	let transitionEndCount = $state(0);

	function calculateTranslates() {
		if (!buttonElement || !textElement || !textElement2) return;

		const buttonWidth = buttonElement.offsetWidth;
		const textWidth = textElement.offsetWidth;

		translateXText1 = buttonWidth + textWidth;
		translateXText2Initial = -(buttonWidth + textWidth);
	}

	async function handleMouseEnter() {
		if (disabled) return;
		
		if (isAnimating) {
			return;
		}
		
		if (isAnimated) {
			isAnimated = false;
			transitionEndCount = 0;
			await tick();
			
			if (textElement && textElement2) {
				textElement.style.transition = 'none';
				textElement2.style.transition = 'none';
				
				textElement.offsetHeight;
				textElement2.offsetHeight;
				
				requestAnimationFrame(() => {
					requestAnimationFrame(() => {
						if (textElement && textElement2) {
							textElement.style.transition = '';
							textElement2.style.transition = '';
							isAnimating = true;
							isAnimated = true;
						}
					});
				});
			}
		} else {
			transitionEndCount = 0;
			isAnimating = true;
			isAnimated = true;
		}
	}
	
	function handleTransitionEnd(e: TransitionEvent) {
		if (e.propertyName === 'transform' && isAnimating) {
			transitionEndCount++;
			if (transitionEndCount >= 2) {
				isAnimating = false;
				transitionEndCount = 0;
			}
		}
	}

	function handleMouseLeave() {
	}

	onMount(() => {
		calculateTranslates();
		window.addEventListener('resize', calculateTranslates);
		return () => {
			window.removeEventListener('resize', calculateTranslates);
		};
	});
</script>

<button
	type={type}
	class="button variant-{baseVariant} {isRounded ? 'rounded' : ''} {className}"
	bind:this={buttonElement}
	{disabled}
	{...rest}
	onmouseenter={handleMouseEnter}
	onmouseleave={handleMouseLeave}
>
	<span
		class="button-text button-text-1 {isAnimated ? 'animate' : ''} speed-{animationSpeed} type-{animationType}"
		bind:this={textElement}
		style="--translate-x-1: {translateXText1}px;"
		ontransitionend={handleTransitionEnd}
	>
		<slot />
	</span>
	<span
		class="button-text button-text-2 {isAnimated ? 'animate' : ''} speed-{animationSpeed} type-{animationType}"
		bind:this={textElement2}
		style="--translate-x-2-initial: {translateXText2Initial}px;"
		ontransitionend={handleTransitionEnd}
	>
		<slot />
	</span>
</button>

<style>
	.button {
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 0.5rem;
		font-weight: 500;
		cursor: pointer;
		border: none;
		outline: none;
		font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
		line-height: 1;
		height: 4rem;
		padding: 0 2rem;
		font-size: 1.4rem;
		text-transform: uppercase;
		background-color: #000000;
		color: #ffffff;
		text-align: center;
		overflow: hidden;
		transition: background-color 0.2s ease-in-out;
	}

	.button.rounded {
		border-radius: 2rem;
	}

	.button.variant-default {
		background-color: #000000;
		color: #ffffff;
		border: none;
	}

	.button.variant-default:hover:not(:disabled) {
		background-color: rgba(0, 0, 0, 0.9);
	}

	.button.variant-outline {
		background-color: transparent;
		color: #000000;
		border: 2px solid #000000;
	}

	.button.variant-outline:hover:not(:disabled) {
		background-color: #000000;
		color: #ffffff;
	}

	.button.variant-destructive {
		background-color: #ef4444;
		color: #ffffff;
		border: none;
	}

	.button.variant-destructive:hover:not(:disabled) {
		background-color: #dc2626;
	}

	.button.variant-ghost {
		background-color: transparent;
		color: #000000;
		border: none;
	}

	.button.variant-ghost:hover:not(:disabled) {
		background-color: rgba(0, 0, 0, 0.05);
	}

	.button-text-1 {
		display: inline-block;
		white-space: nowrap;
		position: static;
		transform: translateX(0);
	}

	.button-text-1.speed-fast {
		transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-1.speed-medium {
		transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-1.speed-slow {
		transition: transform 1.2s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-1.type-arc.speed-fast {
		transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-1.type-arc.speed-medium {
		transition: transform 1.1s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-1.type-arc.speed-slow {
		transition: transform 1.8s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-1.animate {
		transform: translateX(var(--translate-x-1, 0px));
	}

	.button-text-1.type-arc.animate {
		transform: translateX(var(--translate-x-1, 0px)) translateY(50px) rotate(45deg);
	}

	.button-text-2 {
		position: absolute;
		display: inline-block;
		white-space: nowrap;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%) translateX(var(--translate-x-2-initial, 0px));
		opacity: 0;
		pointer-events: none;
	}

	.button-text-2.speed-fast {
		transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.4s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-2.speed-medium {
		transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.7s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-2.speed-slow {
		transition: transform 1.2s cubic-bezier(0.4, 0, 0.2, 1), opacity 1.2s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-2.type-arc.speed-fast {
		transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.7s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-2.type-arc.speed-medium {
		transition: transform 1.1s cubic-bezier(0.4, 0, 0.2, 1), opacity 1.1s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-2.type-arc.speed-slow {
		transition: transform 1.8s cubic-bezier(0.4, 0, 0.2, 1), opacity 1.8s cubic-bezier(0.4, 0, 0.2, 1);
	}

	.button-text-2.animate {
		transform: translate(-50%, -50%) translateX(0);
		opacity: 1;
	}

	.button-text-2.type-arc {
		transform: translate(-50%, -50%) translateX(var(--translate-x-2-initial, 0px)) translateY(50px) rotate(-45deg);
	}

	.button-text-2.type-arc.animate {
		transform: translate(-50%, -50%) translateX(0) translateY(0) rotate(0deg);
		opacity: 1;
	}


	.button:focus-visible {
		outline: 2px solid #000000;
		outline-offset: 2px;
	}

	.button:disabled {
		pointer-events: none;
		opacity: 0.5;
		cursor: not-allowed;
	}
</style>
