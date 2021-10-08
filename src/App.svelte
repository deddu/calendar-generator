<script>
	let caltype = 'weekly';
	import Cal from './Cal.svelte';
</script>

<main>

<label>
	<input type=radio bind:group={caltype} value={'weekly'}>
	weekly
</label>

<label>
	<input type=radio bind:group={caltype} value={'monthly'}>
	monthly
</label>

<label>
	<input type=radio bind:group={caltype} value={'daily'}>
	daily
</label>

	<Cal start='2021-01-01' end='2022-01-01' caltype={caltype}></Cal>
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