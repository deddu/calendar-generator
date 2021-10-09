<script>
	let caltype = 'monthly';
	let start = '2021-01-01';
	let end = '2022-01-01';

	
	import Cal from './Cal.svelte';
</script>

<main>
<header>
	<div>Calendar generator</div>
	
	<label>
		<input type=date disabled bind:value={start}>
		start
	</label>
	<label>
		<input type=date disabled bind:value={end}>
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
	<input type=radio disabled bind:group={caltype} value={'daily'}>
	daily
</label>

	<button disabled>export as pdf</button>

</header>
	<Cal start={start} end={end} caltype={caltype}></Cal>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	header {
		display: flex;
		flex-direction: row;
		justify-content: space-evenly;
	    align-items:center;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>