<script lang="ts">
	import Tile from './Tile.svelte';
	export let tiles: string[];
</script>

<div class="grid">
	{#each tiles as emoji}
		<Tile {emoji} />
	{/each}
</div>

<style>
	.grid {
		display: grid;
		grid-template: repeat(4, 1fr) / repeat(4, 1fr);
		height: 100%;
		gap: 0.5em;
	}
</style>
