<script>
	let calw = 7;
	import Cal from './Cal.svelte';
</script>

<main>

<label>
	<input type=radio bind:group={calw} value={7}>
	weekly
</label>

<label>
	<input type=radio bind:group={calw} value={31}>
	monthly
</label>

<label>
	<input type=radio bind:group={calw} value={1}>
	daily
</label>

	<Cal start='2021-01-01' end='2022-01-01' w={calw}></Cal>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>