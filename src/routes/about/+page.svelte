<script>
	import { page } from '$app/stores';
	import { writable, derived, get } from 'svelte/store';
	import {
		defaultEvmStores,
		web3,
		selectedAccount,
		connected,
		chainId,
		chainData
	} from 'svelte-web3';
	let connectedUser = $selectedAccount || '0x0000000000000000000000000000000000000000';
	// const enableBrowser = () => defaultEvmStores.setBrowserProvider();
	import { onMount } from 'svelte';
	$: balance = $connected ? $web3.eth.getBalance(connectedUser) : ''

	// console.log(wallet_address);

	let user = $selectedAccount;

	// Gift, Yay or Nay ------------------------------------
	let eligibility = true;

	onMount(async () => {
		await fetch(`https://express-api.codeboxxtest.xyz/NFT/gift/${connectedUser}`)
			.then((response) => response.json())
			.then((data) => {
				eligibility = data;
			})
			.catch((error) => {
				console.log("didn't work mate");
				// return [];
			});
	});

	// Check things ----------------------------------
	function elegibityCheck() {
		console.log(eligibility);
		console.log(connectedUser);
		console.log($selectedAccount);
		if (eligibility == false) {
		}
	}

	// Minting that shiet -----------------------------------------
	let apiData = {};
	onMount(async () => {
		await fetch(`https://express-api.codeboxxtest.xyz/NFT/buyWithRocket/${connectedUser}`)
			// fetch(NFTapi)
			.then((response) => response.json())
			.then((data) => {
				apiData = data;
			})
			.catch((error) => {
				console.log('not great');
			});
	});
	console.log(apiData, 'the api thing');

	function test() {
		console.log("I've minted");
		return apiData;
	}

	// function freeNftCheck() {
	// 	onMount(() => {
	// 		// add a test to return in SSR context
	// 		defaultEvmStores.setProvider('https://express-api.codeboxxtest.xyz/NFT/gift/');
	// 	});

	// console.log(wallet_address);
	// fetch('https://express-api.codeboxxtest.xyz/NFT/gift/' + wallet_address)
	// 	.then((response) => response.json())
	// 	.then((data) => console.log(data))
	// 	.catch((err) => console.error(err));
	//}
</script>

<svelte:head>
	<title>Minting Page</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="content">
	<img class="img-present" src="src\images\uncle-monkey.png" alt="" />
	<h1>Uncle Mon(k)ey wants your <strong><em>wallet!</em></strong></h1>
	<p class="motto">We mean, your <strong><em>best</em></strong> interest!</p>
	<p>Connected chain: chainId = {$chainId}</p>
	<p>
		<!-- {checkAccount} Balance on {$chainData.name}: -->
		Your balance on {$chainData.name} server:
		{#await balance}
			<span>waiting...</span>
		{:then value}
			<span>{value}</span>
		{/await}
		{$chainData.nativeCurrency.symbol}
	</p>

	<div class="row">
		<div class="column">
			<img class="img-collect" src="src\images\boredapeyatch.jpg" alt="" />
			<p class="img-collect-text">"The higher mon(k)ey climb, the more you see of its behind."</p>
			<p class="quotees">Albert Einstein, 2022 <br /> <em>(while minting Mon(k)ey)</em></p>
			<button on:click={() => test()}>Mint 'Em</button>
		</div>
		<div class="column">
			<img class="img-collect" src="src\images\RS-BoardApe_Lead_5.webp" alt="" />
			<p class="img-collect-text">"Even mon(k)ey fall from trees."</p>
			<p class="quotees">
				My rich South African mate, 2021 <br /> <em>(watching a monkey falling)</em>
			</p>
		</div>
	</div>

	<div class="btn">
		<button on:click={elegibityCheck} class="cta">You might have freebies here!</button>
	</div>

	<p class="warning-text">
		<em><strong>100%</strong> of the profits will go to people.</em>
	</p>

	<pre>$ sudo give me your mon(k)ey</pre>
</div>

<style>
	.content {
		width: 100%;
		max-width: var(--column-width);
		margin: var(--column-margin-top) auto 0 auto;
	}
	.motto {
		text-align: center;
	}
	.row {
		display: flex;
	}
	.column {
		margin: 0% 2%;
	}
	.img-present {
		position: relative;
		left: 30%;
		width: 40%;
		align-items: center;
		text-align: center;
	}
	.img-collect {
		position: relative;
		width: 100%;
	}
	.img-collect-text {
		font-size: larger;
	}
	.quotees {
		font-size: small;
		font-weight: bold;
		text-align: right;
	}
	.warning-text {
		font-size: 160%;
		text-align: center;
	}

	.btn {
		text-align: center;
	}
</style>
