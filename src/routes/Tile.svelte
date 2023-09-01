<script lang="ts">
	export let emoji: string;
	export let flipped: boolean;
	export let found: boolean;
</script>

<div class="tile" class:flipped>
	{#if !found}
		<button on:click />
		<span>{emoji}</span>
	{/if}
</div>

<style>
	.tile {
		background: yellow;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	button {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	.flipped button {
		background: crimson;
	}

	span {
		font-size: 5em;
		pointer-events: none;
	}
</style>
