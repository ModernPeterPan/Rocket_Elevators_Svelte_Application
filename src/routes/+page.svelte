<script>
	import Counter from '$lib/Counter.svelte';

	function openWallet() {
		let account;
		ethereum.request({method: 'eth_requestAccounts'}).then(accounts => {
			account = accounts[0];
			con
		})
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<div class="container">
		<div class="column center">
			<button on:click={openWallet} class="cta">Don't wait for Mon(k)ey to start</button>
		</div>
		<div class="column">
			<img src="src\images\nft-ape.jpg" alt="" />

			<h2>Ready to make some easy mon(k)ey $</h2>
		</div>
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
