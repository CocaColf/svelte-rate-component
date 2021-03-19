<script>
	import Rate from './Rate.svelte';

	let resultScore = 0;
	let toolTips = ['Very bad', 'bad', 'Normal', 'Good', 'Very good'];

	const onScoreChange = (score) => {
		resultScore = score.detail
	}
</script>

<main>
	<h1 class="test-main">Demo for Rate!</h1>
	<p>The score is: {resultScore}</p>

	<Rate
		allowClear 
		allowHalf 
		on:change={onScoreChange} 
		modelValue={resultScore} 
		toolTips={toolTips} />
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>