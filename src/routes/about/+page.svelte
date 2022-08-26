<script context="module">
	export let hasReceivedFreeNFT = false;
</script>

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
	import { redirect } from '@sveltejs/kit';
	let connectedUser = '0xca782e1f86730b536781a69e93885d1e49c622c1';

	const enableBrowser = () => defaultEvmStores.setBrowserProvider();
	import { onMount } from 'svelte';
	$: balance = $connected ? $web3.eth.getBalance(connectedUser) : '';

	let user = $selectedAccount;

	onMount(async () => {
		await defaultEvmStores.setProvider();
	});
	console.log($selectedAccount);
	console.log(connectedUser);

	// Gift, Yay or Nay -------------------------------------------
	let eligibility = true;

	onMount(async () => {
		await fetch(`https://express-api.codeboxxtest.xyz/NFT/gift/0xca782e1f86730b536781a69e93885d1e49c622c1`)
			.then((response) => response.json())
			.then((data) => {
				eligibility = data;
			})
			.catch((error) => {
				console.log('error with gift eligibility');
				// return [];
			});
	});

	// Check things -----------------------------------------------
	function elegibityCheck() {
		console.log(eligibility);
		console.log(connectedUser);
		console.log($selectedAccount);
		if (eligibility == false) {
			console.log('Fuck U');
		}
	}

	// Whitelisted -------------------------------------------------

	const walletAddress = '0xca782e1f86730b536781a69e93885d1e49c622c1';
	const isWhiteListed = fetch(
		'https://express-api.codeboxxtest.xyz/NFT/addToWhitelist/0xca782e1f86730b536781a69e93885d1e49c622c1',
		{
			method: 'POST',
			headers: {
				accept: 'application/json',
				token: 'RocketElevatorsToTheMoon'
			}
		}
	)
		.then((data) => {
			console.log(data);
			return data;
		})
		.catch((error) => {
			console.log('There was an error');
		});
	//**LOGIC**/
	if (isWhiteListed) {
		console.log('Eligible for free NFT');
	} else {
		console.log('Not Eligible');
		//BONUS//
	}

	function showYouTheFreeNFT() {}

	// Give free kush ----------------------------------------------
	function giveFreeNFT() {
		if (isWhiteListed) {
			console.log('Most Definitly Eligible mate');
			fetch(`https://express-api.codeboxxtest.xyz/NFT/gift/0xca782e1f86730b536781a69e93885d1e49c622c1`, {
				method: 'POST',
				headers: {
					accept: 'application/json'
				}
			})
				.then((data) => {
					console.log(data);
					return data;
				})
				.catch((error) => {
					console.log('You cannot get the Free NFT');
				});

			fetch('https://express-api.codeboxxtest.xyz/NFT/metadata/15', {
				method: 'GET',
				headers: {
					accept: 'application/json'
				}
			})
				.then((data) => {
					console.log(data);
					return data;
				})
				.catch((error) => {
					console.log('There was an error!');
				});
			hasReceivedFreeNFT = true;
			showYouTheFreeNFT();
		} else {
			alert('You are not eligible for a Free NFT!');
		}
	}

	// Minting that shiet -----------------------------------------
	let apiData = {};

	// onMount(async () => {
	// 	await fetch(`https://express-api.codeboxxtest.xyz/NFT/buyWithRocket/${connectedUser}`)
	// 		// fetch(NFTapi)
	// 		.then((response) => response.json())
	// 		.then((data) => {
	// 			apiData = data;
	// 		})
	// 		.catch((error) => {
	// 			console.log('minting is not going great');
	// 		});
	// });
	// console.log(apiData, 'the api thing');

	// function test() {
	// 	console.log("I've minted");
	// }
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
	{#if $connected}
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
	{/if}

	<div class="row">
		<div class="column">
			<img class="img-collect" src="src\images\boredapeyatch.jpg" alt="" />
			<p class="img-collect-text">"The higher mon(k)ey climb, the more you see of its behind."</p>
			<p class="quotees">Albert Einstein, 2022 <br /> <em>(while minting Mon(k)ey)</em></p>
			<button>Mint 'Em</button>
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
		<button on:click={giveFreeNFT} class="cta">You might have freebies here!</button>
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
