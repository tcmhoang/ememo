<script lang="ts">
	import Game from './Game.svelte';
	import '../style.css';
	import Modal from './Modal.svelte';
	import { lvls } from './level';

	let state: 'initial' | 'playing' | 'paused' | 'won' | 'lost' = 'initial';
	let game: Game;
</script>

<Game
	bind:this={game}
	on:win={() => (state = 'won')}
	on:play={() => (state = 'playing')}
	on:lose={() => (state = 'lost')}
	on:pause={() => (state = 'paused')}
/>

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
				<button on:click={() => game.resume()}> resume </button>
				<button on:click={() => (state = 'initial')}> quit </button>
			{:else}
				{#each lvls as lvl}
					<button on:click={() => game.init(lvl)}>
						{lvl.label}
					</button>
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
