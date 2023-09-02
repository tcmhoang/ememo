<script lang="ts">
	import Game from './Game.svelte';
	import '../style.css';
	import Modal from './Modal.svelte';

	let state: 'initial' | 'playing' | 'paused' | 'won' | 'lost' = 'initial';
</script>

<Modal />
