<script lang="ts">
	export let duration: number;
	export let remaining: number;
</script>

<div class="countdown">
	<button>
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
			<title>pause-circle-outline</title>
			<path
				d="M13,16V8H15V16H13M9,16V8H11V16H9M12,2A10,10 0 0,1 22,12A10,10 0 0,1 12,22A10,10 0 0,1 2,12A10,10 0 0,1 12,2M12,4A8,8 0 0,0 4,12A8,8 0 0,0 12,20A8,8 0 0,0 20,12A8,8 0 0,0 12,4Z"
				fill="#999"
			/>
		</svg>
	</button>
	<div class="duration">
		<div class="remaining" style="--r: {remaining / duration}" />
	</div>
</div>

<style>
	.countdown {
		display: flex;
		align-items: center;
		gap: 1em;
	}

	button {
		font-size: 8em;
		width: 1em;
		height: 1em;
		border-color: transparent;
		background-color: transparent;
		border: hidden;
	}

	svg {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
	}

	.duration {
		flex: 1;
		height: 1em;
		background: #ccc;
	}
	.remaining {
		position: absolute;
		height: 100%;
		width: calc(100% * var(--r));
		background-color: #999;
	}
</style>
