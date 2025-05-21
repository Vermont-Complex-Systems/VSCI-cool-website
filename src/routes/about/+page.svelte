<script>
  import Meta from "$lib/components/Meta.svelte";
  import About from "$lib/components/About.svelte";
  import copy from "$data/about.json";

  let { data } = $props();
  const { authors } = data;

  const preloadFont = [
    "https://pudding.cool/assets/fonts/tiempos/TiemposTextWeb-Regular.woff2",
    "https://pudding.cool/assets/fonts/tiempos/TiemposTextWeb-Bold.woff2",
    "https://pudding.cool/assets/fonts/atlas/AtlasGrotesk-Regular-Web.woff2",
    "https://pudding.cool/assets/fonts/atlas/AtlasGrotesk-Bold-Web.woff2",
    "https://pudding.cool/assets/fonts/atlas/AtlasTypewriter-Medium-Web.woff2"
  ];
</script>

<Meta {copy} {preloadFont} />
<About {copy} {authors} />