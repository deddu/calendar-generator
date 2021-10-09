<script>
	let caltype = 'weekly';
	let start = '2021-01-01';
	let end = '2022-01-01';

	
	import Cal from './Cal.svelte';
</script>

<main>

	<label>
		<input type=date bind:value={start}>
		start
	</label>
	<label>
		<input type=date bind:value={end}>
		end
	</label>

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

	<Cal start={start} end={end} caltype={caltype}></Cal>
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