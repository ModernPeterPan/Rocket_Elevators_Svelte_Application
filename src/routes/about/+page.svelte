<script>
	import { defaultEvmStores } from 'svelte-web3';
</script>

<svelte:head>
	<title>Minting Page</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="content">
	<img class="img-present" src="src\images\uncle-monkey.png" alt="" />
	<h1>Uncle Mon(k)ey wants your <strong><em>wallet!</em></strong></h1>
	<p class="motto">We mean, your <strong><em>best</em></strong> interest!</p>

	<div class="row">
		<div class="column">
			<img class="img-collect" src="src\images\boredapeyatch.jpg" alt="">
			<p class="img-collect-text">"The higher mon(k)ey climb, the more you see of its behind."</p>
			<p class="quotees">Albert Einstein, 2022 <br> <em>(while minting Mon(k)ey)</em></p>
		</div>
		<div class="column">
			<img class="img-collect" src="src\images\RS-BoardApe_Lead_5.webp" alt="">
			<p class="img-collect-text">"Even mon(k)ey fall from trees."</p>
			<p class="quotees">My rich South African mate, 2021 <br> <em>(watching a monkey falling)</em></p>
		</div>
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
	.row{
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
</style>
