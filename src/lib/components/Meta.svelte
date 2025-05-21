<script>
  import { page } from "$app/stores";
  let { copy, preloadFont = [] } = $props();
  const base = "https://vermont-complex-systems.github.io/VSCI-cool-website/";
  const url = `${base}${$page.url.pathname}`;
</script>

<svelte:head>
  <title>{copy.title}</title>
  <meta name="description" content={copy.description} />
  <meta name="author" content="The VCSI" />
  <meta name="news_keywords" content={copy.keywords || ""} />

  <meta property="og:title" content={copy.title} />
  <meta property="og:site_name" content="The VCSI" />
  <meta property="og:url" content={url} />
  <meta property="og:description" content={copy.description} />
  <meta property="og:type" content="article" />
  <meta property="og:locale" content="en_US" />

  <meta name="robots" content="max-image-preview:large" />

  <link rel="canonical" href="{url}/" />

  {#each preloadFont as href}
    <link rel="preload" {href} as="font" type="font/woff2" crossorigin />
  {/each}
</svelte:head>
