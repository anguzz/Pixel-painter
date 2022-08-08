<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let selectedColor: string = null;
	export let colors: string[];
	import { setContext } from 'svelte'


	const selectColor = (hex: string) => () => {
		selectedColor = hex;
	};

	const dispatch = createEventDispatcher();
	
	const onAddColor = () => {
		let randomColor = '#';
		for (let i = 0; i < 3; i++) {
			let d = Math.round(Math.random() * 256).toString(16);
			if (d.length < 2) d = '0' + d;
			randomColor += d.toUpperCase();
		}
		const color = prompt('Enter HEX color', randomColor);
		dispatch('addcolor', {
			color
		});
	};
	const removeColor = (color: string) => () => {
		if (confirm(`Are you sure you want to delete ${color}?`))
			dispatch('remcolor', {
				color
			});
	};

	
	import ColorPicker, { Rgb } from 'svelte-awesome-color-picker';

	let rgb: Rgb; // or hsv or hex
	
</script>

<nav>
	
	<ColorPicker bind:rgb />

	<button

		class={selectedColor === null ? 'selected button-icons' : 'button-icons'}
		on:click={selectColor(null)}
		title={'Eraser'}
		>ERASE
	</button>
	{#each colors as hex}
		<button
			style={`background:${hex}`}
			class={hex === selectedColor ? 'selected' : ''}
			on:click={selectColor(hex)}
			title={hex}
		>
			<span title="Delete" class="close" on:click={removeColor(hex)}>&times;</span>
		</button>
	{/each}
	<button on:click={onAddColor} title={'Add color'} class="button-icons">➕</button>
</nav>

<style>
	nav {
		display: flex;
		max-width: 256px;
		flex-wrap: wrap;
		color:#000
	}
	button {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 2.7em;
		height: 2.7em;
		border: 2px solid rgba(255, 255, 255, 1);
		transition: border-color ease 100ms;
		padding: 0.5rem;
		margin: .7px;
		position: relative;
		border-radius: 10px;
	}
	.button-icons {
		color: #000;
		background-color: #e7e7e7;
		display: flex;
		justify-content: center;
		
	}
	button:hover {
		border-color: rgba(255, 255, 255, 0.75);
		transition: border-color ease 100ms;
		cursor: pointer;
		padding:1.55rem;
	}
	button .close {
		opacity: 0;
	}

	button:hover .close {
		opacity: 1;
	}
	button.selected {
		border-color: rgb(12, 182, 212);
		transition: border-color ease 100ms;
		border-width: .3rem;
	}
	button > span.close {
		position: absolute;
		top: -0.5rem;
		right: -0.5rem;
		z-index: 1;
		background: rgba(0, 0, 0, 0.25);
		border-radius: 0.5rem;
		color: white;
		width: 1rem;
		height: 1rem;
		display: flex;
		padding-left: 1px;
		font-size: 1.25rem;
		font-weight: normal;
		line-height: 1rem;
		align-items: center;
		justify-content: center;
		text-align: center;
	}
</style>
