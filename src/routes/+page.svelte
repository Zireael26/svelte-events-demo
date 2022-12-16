<script lang="ts">
	import Product from '../components/Product.svelte';

	let products = [
		{ id: 'p1', title: 'A Book', price: 10.99 },
		{ id: 'p2', title: 'A Carpet', price: 89.99 }
	];

	function addToCart(event: CustomEvent) {
		console.log('Add to cart: ', event);
	}

	function deleteProduct(event: CustomEvent) {
		console.log('Delete Product', event);
	}
</script>

{#each products as product (product.id)}
	<Product {...product} on:add-to-cart={addToCart} on:delete-product={deleteProduct} />
{/each}
