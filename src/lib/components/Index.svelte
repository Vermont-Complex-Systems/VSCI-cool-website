<script>
	import { getContext } from "svelte";
	import Footer from "$lib/components/Footer.svelte";
	import Hero from "$lib/components/Hero.svelte";
	import CMS from "$lib/components/helpers/CMS.svelte";

	const copy = getContext("copy");
	const { body } = copy;
	const components = { Hero };
</script>

<div id="story">
	<CMS {body} {components}></CMS>
</div>

<svelte:boundary onerror={(e) => console.error(e)}>
	<Footer recirc={true} />
</svelte:boundary>

<style>
	:global(#story section) {
		padding: 0 16px;
	}

	:global(#story section > *) {
		display: block;
		margin: 32px auto;
		max-width: var(--col-width);
	}

	:global(#story section aside, #story section code) {
		background: var(--color-bg-alt);
		padding: 16px;
	}

	:global(#stroy span.emoji) {
		display: block;
		text-align: center;
		font-size: 2em;
	}

	:global(#story section code) {
		text-align: center;
	}

	:global(#story section span.center) {
		display: block;
		text-align: center;
	}

	:global(#story section span.emoji) {
		display: block;
		text-align: center;
		font-size: 2.5em;
		line-height: 1;
	}

	:global(#story section strong.big) {
		font-size: 2em;
		line-height: 1.2;
	}

	:global(#story section img) {
		width: 100%;
	}

	:global(#story section img.emoji) {
		max-width: 64px;
	}
</style>
