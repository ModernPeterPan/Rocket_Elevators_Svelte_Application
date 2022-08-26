<script>
	import {
		defaultEvmStores,
		web3,
		selectedAccount,
		connected,
		chainId,
		chainData
	} from 'svelte-web3';
	import { writable, derived, get } from 'svelte/store';
	import { onMount } from 'svelte';
	import { redirect } from '@sveltejs/kit';
	const enableBrowser = () => defaultEvmStores.setProvider();
	let connectedUser = '0xca782e1f86730b536781a69e93885d1e49c622c1';
	
	$: balance = $connected ? $web3.eth.getBalance(connectedUser) : '';


	onMount(async () => {
        await defaultEvmStores.setProvider()})
	// -------------------------------eligibility API------------------------
	let eligibility = true;
	

	function redirectMintPage() {
		window.location.replace('/about');
		console.log(connectedUser);
		console.log($selectedAccount);
	}

	onMount(async () => {
		await fetch(`https://express-api.codeboxxtest.xyz/NFT/gift/${connectedUser}`)
			.then((response) => response.json())
			.then((data) => {
				eligibility = data;
			})
			.catch((error) => {
				console.log('error with gift eligibility');
				// return [];
			});
	});

	function test() {
		console.log($selectedAccount);
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<div class="container">
		<div class="column center">
			<button on:click={enableBrowser} on:click={redirectMintPage} class="cta"
				>Don't wait for your Mon(k)ey come see the NFTs!</button
			>
			<button on:click={test} class="cta">test here</button>
		</div>
		<div class="column">
			<img src="src\images\nft-ape.jpg" alt="" />

			<h2>Ready to make some easy mon(k)ey $</h2>
		</div>
		<p>
			Connected: {$connected || 'not defined'}
		</p>
	</div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	.container {
		position: relative;
		display: flex;
		flex-direction: row;
		text-align: center;
	}

	.column {
		width: 50%;
	}

	.container img {
		width: 100%;
	}

	.cta {
		padding: 15px 30px;
	}

	.center {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
