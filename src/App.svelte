<script>
	import Loader from './Loader.svelte';
	import WordData from './WordData.svelte';

	let word = '';
	let loading = false;
	let wordData = null;

	async function searchWord() {
		if (word.length === 0) {
			return;
		}
		loading = true;
		wordData = null;
		try {
			let res = await fetch(
				'https://api.dictionaryapi.dev/api/v2/entries/en/' + word
			);
			let data = await res.json();
			if (Array.isArray(data)) {
				wordData = data[0];
			} else {
				wordData = 'No results';
			}
			loading = false;
		} catch (err) {
			loading = false;
			// console.log(err);
		}
	}

	// gsap
	// gsap.from('.slide-right', {
	// 	opacity: 0,
	// 	x: -300,
	// 	duration: 1,
	// });
</script>

<style>
	.header {
		margin-bottom: 2rem;
		padding: 20px;
		font-size: 1.6rem;
		font-weight: bold;
		background-color: #111;
		color: #f5f5f5;
	}
	.center {
		margin: 40px auto;
		width: 95%;
		max-width: 550px;
		background: #fff;
		box-shadow: 2px 5px 8px rgba(0, 0, 0, 0.5);
	}
	.form {
		background-color: #fff;
		margin: 20px 0;
		padding: 20px;
		border: 1px solid #f5f5f5;
		box-shadow: 0 0 5px 2px rgba(0, 0, 0, 0, 0.05);
	}
	.form .form-group {
		margin: 10px 0;
	}
	.form .form-group label {
		display: block;
		margin-bottom: 8px;
		font-size: 16px;
	}
	.form .form-group input {
		width: 100%;
		padding: 10px;
		font-size: 1rem;
		border: 1px solid #bbb;
	}
	.form .form-group button {
		padding: 10px 20px;
		background-color: #111;
		color: #f5f5f5;
		border: none;
		outline: none;
		cursor: pointer;
	}
	.form .form-group button:hover {
		background-color: #2f2f2f;
	}
	.result {
		background-color: #fff;
		border: 1px solid #f5f5f5;
		box-shadow: 0 0 5px 2px rgba(0, 0, 0, 0.05);
	}
	.result .padding {
		padding: 20px;
	}
</style>

<main>
	<header class="header">Svelte Dictionary App</header>
	<div class="center">
		<div class="form">
			<div class="form-group">
				<label for="word">Search Word</label>
				<input
					type="text"
					name="word"
					placeholder="Type word here"
					bind:value={word}
				/>
			</div>
			<div class="form-group">
				<button on:click={searchWord}>Search</button>
			</div>
		</div>
		{#if loading === true || wordData !== null}
			<div class="result">
				{#if wordData !== null && typeof wordData !== 'string'}
					<WordData {wordData} />
				{:else if wordData === null && loading === true}
					<Loader />
				{:else}
					<p class="padding">No result found</p>{/if}
			</div>
		{/if}
	</div>
</main>
