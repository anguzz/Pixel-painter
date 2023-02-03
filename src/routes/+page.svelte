<script lang="ts" context="module">
 
</script>

<script lang="ts">
  import SEO from "svelte-seo";
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



<Content backgroundClass={neutralBackground} />

<Footer backgroundClass={neutralBackground} />

<style>
	

</style>