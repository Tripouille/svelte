<script>
	let name = 'Yoshi';
	let beltColour = 'black';

	const handleInputChange = (e) => {
		beltColour = e.target.value;
	};
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>{beltColour} belt</p>
	<input type='text' value={beltColour} on:input={handleInputChange}/>
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