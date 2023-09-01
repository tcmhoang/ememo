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

<div class="tile" class:flipped>
	{#if !found}
		<button on:click />
		<img src={toSvgPath(emoji)} alt={emoji} />
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

	img {
		width: 6em;
		height: 6em;
		pointer-events: none;
	}
</style>
