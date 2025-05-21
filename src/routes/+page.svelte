<script>
  import { setContext } from "svelte";
  import { browser } from "$app/environment";
  import Meta from "$lib/components/Meta.svelte";
  import Home from "$lib/components/Home.svelte";

  // import HiddenAuthors from "$lib/components/HiddenAuthors.svelte";
  import version from "$lib/utils/version.js";
  import copy from "$data/home.json";

  let { data } = $props();

  version();

  const preloadFont = [
    "https://vermont-complex-systems.github.io/VSCI-cool-website/assets/fonts/tiempos/TiemposTextWeb-Regular.woff2",
    "https://vermont-complex-systems.github.io/VSCI-cool-website/assets/fonts/tiempos/TiemposTextWeb-Bold.woff2",
    "https://vermont-complex-systems.github.io/VSCI-cool-website/assets/fonts/atlas/AtlasGrotesk-Regular-Web.woff2",
    "https://vermont-complex-systems.github.io/VSCI-cool-website/assets/fonts/atlas/AtlasGrotesk-Bold-Web.woff2",
    "https://vermont-complex-systems.github.io/VSCI-cool-website/assets/fonts/atlas/AtlasTypewriter-Medium-Web.woff2"
  ];

  const { stories, staff } = data;

  const { title, description, url, keywords } = copy;

  setContext("Home", { stories, copy, staff });
</script>

<Meta {copy} {preloadFont} />
<Home />
