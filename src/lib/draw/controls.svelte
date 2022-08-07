<script lang="ts">
	import { ImageType } from './types';
	export let saveImage = (_type: ImageType) => {};
	export let gridEnabled = true;


	const toggleGrid = () => (gridEnabled = !gridEnabled);

	
 
</script>

<nav class="toggles">
	
	<button
		title={`Toggle Grid`}
		on:click={toggleGrid}
		class={gridEnabled ? 'toggle active' : 'toggle'}
	>
		<span>GRID</span>
	</button>
</nav>
<slot />
<nav>
	{#each ['png', 'svg'] as ext}
		<button on:click={() => saveImage(ImageType[ext])}>Save as {ext.toUpperCase()}</button>
	{/each}
</nav>

<style>
	nav {
		display: grid;
		grid-gap: 1rem;
		align-items: center;
		margin: 0 auto;
		grid-template-columns: repeat(5, 1fr);
		
	}
	nav.toggles {
		grid-template-columns: repeat(3, 1fr);
	}
	button {
		background-color: #3a8ccf;
		border: none;
		border-radius: 10px;
	}
	.active {
		background-color: #606c76;
	}
	button.toggle {
		border: 1px solid rgba(0, 0, 0, 0.08);
		background: #1f2937;
		border-radius: 2rem;
		width: 8rem;
		padding: 0 4rem 0 0;
		height: 4rem;
		display: inline-flex;
		transition: padding ease 300ms;
		margin-left:40rem;
	}
	.toggle > span {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 4rem;
		height: 4rem;
		border-radius: 4rem;
		background-color: #1362bd;
		transition: background-color ease 300ms;
	}
	.toggle.active {
		padding-right: 0;
		padding-left: 4rem;
		transition: padding ease 300ms;
	}
	.toggle.active > span {
		background-color: #1362bd;
		transition: background-color ease 300ms;
	}
</style>
