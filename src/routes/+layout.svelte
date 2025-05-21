<script lang="ts">
	import '$styles/app.css';
	import Header from "$lib/components/Header.svelte";

	let { children } = $props();
</script>

<Header />
<main id="content">
	{@render children?.()}
</main>