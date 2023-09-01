<script lang="ts">
	import { onMount } from 'svelte';
	import Page from './+page.svelte';
	import Countdown from './Countdown.svelte';
	import Found from './Found.svelte';
	import Grid from './Grid.svelte';
	import { lvls, type Level } from './level';

	const lvl: Level = lvls[0];
	let isPlayingState = true;

	const tiles: string[] = initPairs(lvl.emojis, lvl.size ** 2 / 2);
	let found: string[] = [];

	function initPairs(emojis: string[], size: number) {
		let cpemojis: string[] = [...emojis];

		function removeAt(index: number) {
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
	const duration = lvl.duration;
	let remaining = lvl.duration;

	function countdown() {
		const start = Date.now();
		let remainingOnPaused = remaining;

		function loop() {
			if (!isPlayingState) return;
			requestAnimationFrame(loop);
			remaining = remainingOnPaused - (Date.now() - start);

			if (remaining <= 0) {
				// end
				isPlayingState = false;
			}
		}
		loop();
	}
	onMount(countdown);
</script>

<div class="game">
	<div class="info">
		<Countdown {remaining} {duration} />
	</div>
	<div class="game-container">
		<Grid {tiles} on:found={(e) => (found = [...found, e.detail])} {found} />
	</div>
	<div class="info">
		<Found {found} />
	</div>
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
	}
	.game-container {
		width: 80em;
		height: 80em;
	}
</style>
