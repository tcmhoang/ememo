<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import Countdown from './Countdown.svelte';
	import Found from './Found.svelte';
	import Grid from './Grid.svelte';
	import type { Level } from './level';

	const dispatch = createEventDispatcher();

	let isPlayingState: boolean = true;

	let size: number = 0;
	let remaining: number = 0;
	let pairCount: number = 0;
	let duration: number = 0;
	let tiles: { e: string; id: string }[] = [];
	let found: string[] = [];

	export function init(lvl: Level) {
		size = lvl.size;
		pairCount = size ** 2 / 2;
		tiles = initPairs(lvl.emojis, pairCount);
		duration = remaining = lvl.duration;
		resume();
	}

	export function resume() {
		isPlayingState = true;
		countdown();

		dispatch('play');
	}

	function countdown() {
		const start = Date.now();
		let remainingOnPaused = remaining;

		function loop() {
			if (!isPlayingState) return;
			requestAnimationFrame(loop);
			remaining = remainingOnPaused - (Date.now() - start);

			if (remaining <= 0) {
				isPlayingState = false;
				dispatch('lose');
			}
		}
		loop();
	}

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

		return [
			...randomSet.map((e) => ({ e, id: `${e}:a` })),
			...randomSet.map((e) => ({ e, id: `${e}:b` }))
		]
			.map((e) => ({ e, sort: Math.random() }))
			.sort((a, b) => a.sort - b.sort)
			.map(({ e }) => e);
	}
</script>

<div class="game" style="--size: {size}">
	<div class="info">
		<Countdown
			{remaining}
			{duration}
			on:click={() => {
				isPlayingState = false;
				dispatch('pause');
			}}
		/>
	</div>
	<div class="game-container">
		<Grid
			{tiles}
			on:found={(e) => {
				found = [...found, e.detail];
				if (found.length == pairCount) {
					dispatch('win');
				}
			}}
			{found}
			{size}
		/>
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
