<script lang="ts">
	import Grid from './Grid.svelte';
	import { lvls } from './level';

	const tiles: string[] = initPairs(lvls[0].emojis, lvls[0].size ** 2 / 2);
	let found: string[] = [];

	function initPairs(emojis: string[], size: number) {
		let cpemojis: string[] = [...emojis];

		function removeAt(index: number) {
			console.log('called');
			const idx: number = Math.floor(index);
			const validatedIdx: number =
				idx > cpemojis.length - 1 ? cpemojis.length - 1 : idx;
			const o: string = cpemojis[validatedIdx];
			cpemojis.splice(validatedIdx, 1);
			return o;
		}

		const randomSet: string[] = [...Array(size)].map((_) =>
			removeAt(Math.random() * (cpemojis.length - 1))
		);

		return [...randomSet, ...randomSet]
			.map((e) => ({ e, sort: Math.random() }))
			.sort((a, b) => a.sort - b.sort)
			.map(({ e }) => e);
	}
</script>

<div class="game">
	<div class="info" />
	<div class="game-container">
		<Grid {tiles} />
	</div>
	<div class="info" />
</div>

<style>
	.game {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100%;
		font-size: min(1vmin, 0.3rem);
	}
	.info {
		width: 80em;
		height: 10em;
		background: purple;
	}
	.game-container {
		width: 80em;
		height: 80em;
		background: teal;
	}
</style>