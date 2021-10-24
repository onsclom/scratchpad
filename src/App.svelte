<script>
	import { onMount } from 'svelte';
	import { scale, blur, fade } from 'svelte/transition';

	let text = ""
	let visible = false
	onMount(async () => {
		if (localStorage.getItem('text') != null) {
			text = localStorage.getItem('text')
		} else {
			text = `                _       _     
  ___  ___ _ __| |_ ___| |__  
 / __|/ __| '__| __/ __| '_ \\ 
 \\__ \\ (__| |  | || (__| | | |
 |___/\\___|_|   \\__\\___|_| |_|
 
Changes automatically save in your browser's local storage!
 
Pro tip: Make a bookmark of this page to use it as a scratch pad.`
		}

		visible = true
	});

	function saveToLocalStorage() {
		localStorage.setItem('text', text)
	}
</script>

<main>

	{#if visible}
	<textarea transition:blur="{{duration: 2000}}" bind:value={text} on:input={saveToLocalStorage}></textarea>
	{/if}
</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono&display=swap');

	main {
		width: 100%;
		height: 100%;
	}

	textarea {
		display: block;
		width: 100%;
		height: 100%;
		box-sizing: border-box;
		margin: 0;
		padding: 0;
		outline: none;
		resize: none;
		border: 1px solid var(--text-color);
		padding: 1em;
		background-color: var(--bg-color);
		color: var(--text-color);
		font-family: 'IBM Plex Mono', monospace;
	}
</style>