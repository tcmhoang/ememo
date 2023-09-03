<div class="background">
	<div class="modal">
		<slot />
	</div>
</div>

<style>
	.background {
		position: fixed;
		width: 100%;
		height: 100%;
		backdrop-filter: blur(10px);
		display: grid;
		place-items: center;
		z-index: 999;
		top: 0;
		left: 0;
	}
</style>
