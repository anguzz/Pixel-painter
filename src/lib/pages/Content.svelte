<script lang="ts">
  import Page from "$lib/components/Page.svelte";
  import { primaryBackground } from "$lib/utils/constants";

 	 export let backgroundClass = primaryBackground;
  	import Controls from "$lib/draw/controls.svelte";
 	 import DrawingBoard from "$lib/draw/drawing-board.svelte";
 	 import { downloadURI } from "$lib/draw/files";
	import Palette from "$lib/draw/palette.svelte";
	import {  ColoredPixels,ImageDataType, ImageType } from "$lib/draw/types";
  	import type { ImageDataFn } from "$lib/draw/types";
   import pixelsToSVG from '$lib/draw/pixelsToSVG';


	let gridEnabled = true;
	let colors = [
'#000000', '#FFFFFF', '#C0C0C0', 
'#FF0000','#800000','#008080','#FF00FF',
'#0000FF','#000080','#00FFFF','#73DE8C',
'#808000','#00FF00','#008000','#FFFF00'

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

 
  <Controls bind:gridEnabled {saveImage}>
    <Palette {colors} bind:selectedColor on:addcolor={addColor} on:remcolor={removeColor} />
    <DrawingBoard bind:color={selectedColor} {gridEnabled} bind:getImageData />
  </Controls>
</Page>


<style>


</style>