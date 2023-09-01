<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import Tile from './Tile.svelte';

	export let tiles: string[];
	export let found: string[];

	let dispatcher = createEventDispatcher();

	let selected = new Set<Number>();
	let timeoutPid: number | null;

	function onTileClick(i: number) {
		if (timeoutPid != null) {
			clearTimeout(timeoutPid);
			timeoutPid = null;
			selected.clear();
		}
		selected.add(i);
		console.log(selected);

		if (selected.size == 2) {
			const [a, b] = [...selected];
			if (tiles[+a] == tiles[+b]) {
				selected.clear();
				dispatcher('found', tiles[+a]);
			} else {
				timeoutPid = setTimeout(() => {
					selected.clear();
					selected = selected;
					timeoutPid = null;
				}, 1000);
			}
		}

		selected = selected;
	}
</script>

<div class="grid">
	{#each tiles as emoji, i}
		<Tile
			{emoji}
			flipped={selected.has(i)}
			on:click={() => onTileClick(i)}
			found={found.includes(tiles[i])}
		/>
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
