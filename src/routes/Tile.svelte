<script lang="ts" context="module">
	export function toSvgPath(emoji: string) {
		return `/twemoji/${[...emoji]
			.map((c) => c.codePointAt(0)!.toString(16))
			.join('-')}.svg`;
	}
</script>

<script lang="ts">
	export let emoji: string;
	export let flipped: boolean;
	export let found: boolean;
</script>

<div class="tile" class:flipped={flipped || found}>
	<button on:click />
	{#if !found}
		<img src={toSvgPath(emoji)} alt={emoji} />
	{/if}
</div>

<style>
	.tile {
		display: flex;
		justify-content: center;
		align-items: center;
		transition: transform 0.3s;
		transform-style: preserve-3d;
	}

	button {
		position: absolute;
		width: 100%;
		height: 100%;
		backface-visibility: hidden;
		background-color: #eee;
		border: hidden;
		border-radius: 1em;
		font-size: inherit;
	}

	.flipped {
		border-radius: 1em;
		border: 0.5em solid #eee;
		background-color: #fff;
		transform: rotateY(180deg);
	}

	img {
		width: 6em;
		height: 6em;
		pointer-events: none;
		transform: rotateY(180deg);
		backface-visibility: hidden;
	}
</style>
