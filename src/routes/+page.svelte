<script lang="ts">
	import Game from './Game.svelte';
	import '../style.css';
	import Modal from './Modal.svelte';
	import { lvls } from './level';

	let state: 'initial' | 'playing' | 'paused' | 'won' | 'lost' = 'initial';
</script>

<Game />

{#if state != 'playing'}
	<Modal>
		<header>
			<h1>E<span>nemo</span></h1>
			<p>The emoji matching game</p>
		</header>
		{#if state == 'won' || state == 'lost'}
			<p>You {state} the game!</p>
		{:else if state == 'paused'}
			<p>Game paused</p>
		{:else if state == 'initial'}
			<p>Choose a level:</p>
		{/if}

		<div class="buttons">
			{#if state == 'paused'}
				<button>resume</button>
				<button>quit</button>
			{:else}
				{#each lvls as lvl}
					<button>{lvl.label}</button>
				{/each}
			{/if}
		</div>
	</Modal>
{/if}

<style>
	h1 {
		font-size: 4em;
		color: dimgray;
	}
	h1 span {
		color: orchid;
	}

	p {
		font-family: emilys-candy;
	}
</style>
