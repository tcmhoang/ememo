<script lang="ts">
	import { toSvgPath } from './Tile.svelte';
	export let found: string[];
</script>

<div class="found">
	{#each found as emoji (emoji)}
		<img src={toSvgPath(emoji)} alt={emoji} />
	{/each}
</div>

<style>
	.found {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.5em;
	}
	img {
		width: 4em;
		height: 4em;
	}
</style>
