<script>
	import Counter from '$lib/Counter.svelte';
	let connectedUser = '0xca782e1f86730b536781a69e93885d1e49c622c1';
	import { onMount } from 'svelte';

	// import {hasReceivedFreeNFT} from $./+page.svelte;

	/** @type {import('./$types').PageData} */
	export let data;
	let hasReceivedFreeNFT = false;

	onMount(async () => {
		if (connectedUser == '0xca782e1f86730b536781a69e93885d1e49c622c1') {
			let hasReceivedFreeNFT = true;
		}
	});

	console.log("https://ipfs.moralis.io:2053/ipfs/Qma342PQhNdpmPXkv4K3gELngG1nPUD9224XNSst6RYqsr/RocketElevatorsNFTImage_15.png")
</script>

<svelte:head>
	<title>Porte-folies-o</title>
	<meta name="description" content="A todo list app" />
</svelte:head>

<div class="todos">
	<h1>You'd be crazy not to invest more.</h1>
	<img src="src\images\scarface.jpg" alt="" />
	<p>Who you could become with maybe <strong><em>just</em></strong> one more collection.</p>
</div>
<div class="NFT">
	<img
		src="https://ipfs.moralis.io:2053/ipfs/Qma342PQhNdpmPXkv4K3gELngG1nPUD9224XNSst6RYqsr/RocketElevatorsNFTImage_15.png"
		alt="A ugly house drew by a 5 years old. Hoping, you didn't pay too much."
	/>
	<p>Your free NFT</p>
</div>

<style>
	.todos {
		width: 100%;
		max-width: var(--column-width);
		margin: auto auto;
		text-align: center;
	}

	.NFT p {
		text-align: center;
	}

	img {
		width: 70%;
	}

	.NFT img {
		width: 30%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		margin: auto auto;
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
