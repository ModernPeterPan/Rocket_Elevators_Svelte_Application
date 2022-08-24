<script>
	import { enhance } from '$lib/form';
	import { scale } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	/** @type {import('./$types').PageData} */
	export let data;
</script>

<svelte:head>
	<title>Todos</title>
	<meta name="description" content="A todo list app" />
</svelte:head>

<div class="todos">
	<h1>You'd be crazy not to invest more.</h1>
	<img src="src\images\scarface.jpg" alt="">
	<p>Who you could become with maybe <strong><em>just</em></strong> one more collection.</p>
</div>

<style>
	.todos {
		width: 100%;
		max-width: var(--column-width);
		margin : auto auto;
		text-align: center;
	}

	img {
		width: 70%;
	}

	.new {
		margin: 0 0 0.5rem 0;
	}

	input {
		border: 1px solid transparent;
	}

	input:focus-visible {
		box-shadow: inset 1px 1px 6px rgba(0, 0, 0, 0.1);
		border: 1px solid #ff3e00 !important;
		outline: none;
	}

	.new input {
		font-size: 28px;
		width: 100%;
		padding: 0.5em 1em 0.3em 1em;
		box-sizing: border-box;
		background: rgba(255, 255, 255, 0.05);
		border-radius: 8px;
		text-align: center;
	}
</style>
