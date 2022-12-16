<script lang="ts">
	import Modal from '../components/Modal.svelte';
	import Product from '../components/Product.svelte';

	let products = [
		{ id: 'p1', title: 'A Book', price: 10.99 },
		{ id: 'p2', title: 'A Carpet', price: 89.99 }
	];

	let showModal = false;

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

<button on:click={() => (showModal = true)}>Show Modal</button>
{#if showModal}
	<Modal on:close={() => (showModal = false)} on:cancel={() => (showModal = false)}>
		<header slot="header">Here is a header</header>
		<h2>Here is some content</h2>
		<p>Here is some more content</p>
		<!-- <p slot="footer">Here is a footer</p> -->
	</Modal>
{/if}
