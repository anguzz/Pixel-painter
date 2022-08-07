<script lang="ts" context="module">
 
</script>

<script lang="ts">
  import SEO from "svelte-seo";
  import Home from "$lib/pages/Home.svelte";
  import Content from "$lib/pages/Content.svelte";
import Footer from "$lib/pages/Footer.svelte";

/* basic colors at  https://tailwindcss.com/docs/customizing-colors   more at  https://hypercolor.dev/   */ 
  let primaryBackground = "bg-gradient-to-r from-slate-900 to-blue-900";
  let neutralBackground = "bg-neutral-200 dark:bg-neutral-900";
</script>

<SEO
  title="Pixel-painter"
  description="Draw some pixel art and save it!"
  canonical="site link"
/>

<Home />

<Content backgroundClass={neutralBackground} />

<Footer backgroundClass={neutralBackground} />

<style>
	

</style>