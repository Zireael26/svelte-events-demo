<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	export let id: string;
	export let title: string;
	export let price: number;
	export let bestseller = false;

	const dispatch = createEventDispatcher();

	function addToCart() {
		dispatch('add-to-cart', { id: id });
	}
</script>

<article>
	<h1>{title}</h1>
	<h2>${price}</h2>
	{#if bestseller}
		<h3>Bestseller!</h3>
	{/if}
	<button on:click={addToCart}>Add to Cart</button>
	<button
		on:click={() => {
			dispatch('delete-product', id);
		}}>Delete</button
	>
</article>
