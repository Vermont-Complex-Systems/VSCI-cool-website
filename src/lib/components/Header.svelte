<script>
	// shadow, plain, line, bubble
  	import wordmark from '$lib/assets/wordmark-sticker.svg';
</script>

<header>
	<div class="wordmark">
		<a href="https://pudding.cool/" aria-label="The Pudding" target="_self">
      		<img src={wordmark} alt="The Pudding" />
    	</a>
	</div>
	<p class="byline">
		<small>
			By <a
				target="_blank"
				rel="noreferrer"
				href="https://pudding.cool/author/russell-samora/">Jonathan St-Onge</a
			></small
		>
	</p>
</header>

<style>
	.wordmark {
		max-width: 14em;
		margin: 0 auto;
		padding: 32px 0;
		transform: rotate(-4deg);
	}

	.wordmark a {
		border: none;
		display: block;
		color: var(--color-fg);
	}

	.wordmark a:hover {
		background-color: transparent;
	}

	.byline {
		position: absolute;
		top: 16px;
		right: 16px;
		margin: 0;
		line-height: 1;
	}

	@media (max-width: 600px) {
		.byline {
			position: relative;
			top: 12px;
		}

		header {
			display: flex;
			justify-content: space-between;
			align-items: flex-start;
		}

		.wordmark {
			margin: 0;
			padding: 16px;
			max-width: 10em;
		}
	}
</style>
