<script lang="ts">
  import Page from "$lib/components/Page.svelte";
  import { primaryBackground } from "$lib/utils/constants";
  import Controls from "$lib/draw/controls.svelte";
  import DrawingBoard from "$lib/draw/drawing-board.svelte";
  import { downloadURI } from "$lib/draw/files";
  import Palette from "$lib/draw/palette.svelte";
  import {  ColoredPixels,ImageDataType, ImageType } from "$lib/draw/types";
  import type { ImageDataFn } from "$lib/draw/types";
  import pixelsToSVG from '$lib/draw/pixelsToSVG';
  import Text from "$lib/components/Text.svelte";
  export let backgroundClass = primaryBackground;



	let gridEnabled = true;
	let colors = [
'#000000', '#FFFFFF', '#C0C0C0', '#FF0000',
'#bc45f8','#0000FF',
'#008000','#FFFF00'

];
	let selectedColor = colors[0];
	let getImageData: ImageDataFn = () => '';

	const saveImage = (type: ImageType) => {
		let filename = prompt('Name your drawing!', 'image');
		if (!filename.endsWith('.' + type)) filename += '.' + type;
		switch (type) {
			case ImageType.png:
				return downloadURI(getImageData(ImageDataType.url) as string, filename);
			case ImageType.svg:
				return downloadURI(
					pixelsToSVG(getImageData(ImageDataType.pixels) as ColoredPixels),
					filename
				);
			default:
				throw Error(`Image type ${type} is not implemented`);
		}
	};

	const addColor = (e: { detail: { color: string } }) => {
		const color = e.detail.color;
		colors = [...new Set([...colors, color])];
	};
	const removeColor = (e: { detail: { color: string } }) => {
		const set = new Set([...colors]);
		set.delete(e.detail.color);
		colors = [...set];
	};


</script>



<title>Content</title>
<Page id="Content" title=" " {backgroundClass}>
	<div
  class="flex flex-col items-center justify-center bg-center bg-no-repeat bg-cover page lg:bg-fixed bg-neutral-600 bg-blend-soft-light dark:bg-blend-soft-light dark:bg-neutral-700"
  id="bg"
>
<Text>
	<h1 class="text-5xl m-6  font-light"> 👾 Pixel-Painter 🔹 </h1>

  <Controls bind:gridEnabled {saveImage}>
	<br>
    <Palette {colors} bind:selectedColor on:addcolor={addColor} on:remcolor={removeColor} />
	<br>
    <DrawingBoard bind:color={selectedColor} {gridEnabled} bind:getImageData />
  </Controls>
</Text>
</div>
</Page>

 

<style>

#bg {
    /* The image used background-image: url("/assets/images/background1.jpg"); */
    background-image: linear-gradient(217deg, rgba(0, 178, 248, 0.8), rgba(255,0,0,0) 70.71%),
      linear-gradient(127deg, rgba(212, 0, 255, 0.8), rgba(0,255,0,0) 70.71%),
      linear-gradient(336deg, rgba(248, 248, 248, 0.8), rgba(0,0,255,0) 70.71%);
    
  }
</style>