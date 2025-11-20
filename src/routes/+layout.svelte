<script lang="ts">
	let { children } = $props();
</script>

<style>
	:global(body) {
		background-color: #fefefe;
		margin: 0;
		padding: 0;
		min-height: 100vh;
	}
</style>

{@render children()}
