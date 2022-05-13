<script>
	import { fly } from 'svelte/transition';
	export let wordData = null;

	function playAudio(src) {
		let audio = '';
		audio = new Audio(src);
		audio.play();
	}
</script>

<style>
	.word-data .audios {
		border-bottom: 1px solid #f5f5f5;
	}
	.word-data .audios .audio {
		padding: 8px 20px;
	}
	.word-data .audios .audio i {
		cursor: pointer;
	}
	.word-data .meaning {
		padding: 0 20px;
		border-bottom: 1px solid #f5f5f5;
	}
	.word-data > div:last-child {
		border-bottom: none;
	}
	.word-data .meaning .part-of-speech {
		margin: 10px 0 0;
		font-size: 18px;
		font-weight: 600;
	}
	.word-data .meaning .definitions .definition {
		padding: 8px 0;
	}
	.word-data .meaning .definitions .definition p {
		margin: 5px 0;
	}
</style>

<div class="word-data">
	{#if wordData.phonetics}
		<div class="audios">
			{#each wordData.phonetics as data}
				<div
					class="audio"
					transition:fly={{ x: -400, opacity: 0, duration: 300 }}
				>
					<p>{data.text}</p>
					<i
						class="fa-solid fa-circle-play"
						on:click={() => playAudio(data.audio)}
					/>
				</div>
			{/each}
		</div>
	{/if}
	{#each wordData.meanings as meaning}
		<div
			class="meaning"
			transition:fly={{ x: 400, opacity: 0.5, duration: 500 }}
		>
			<div class="part-of-speech">&bull; {meaning.partOfSpeech}</div>
			<div class="definitions">
				{#each meaning.definitions as data}
					<div class="definition">
						<p>Definition: <b>{data.definition}</b></p>
						{#if data.example}
							<p>Example: <i>{data.example}</i></p>
						{/if}
					</div>
				{/each}
			</div>
		</div>
	{/each}
</div>
