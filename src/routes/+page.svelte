<script lang="ts">
	import { tick } from 'svelte';
	import Modal from '../components/Modal.svelte';
	import Product from '../components/Product.svelte';

	let products = [
		{ id: 'p1', title: 'A Book', price: 10.99 },
		{ id: 'p2', title: 'A Carpet', price: 89.99 }
	];

	let showModal = false;
	let text = 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quod.';

	function addToCart(event: CustomEvent) {
		console.log('Add to cart: ', event);
	}

	function deleteProduct(event: CustomEvent) {
		console.log('Delete Product', event);
	}

	function transformText(event: KeyboardEvent) {
		if (event.key !== 'Tab') {
			return;
		}
		event.preventDefault();

		const selectionStart = (event.target as HTMLTextAreaElement).selectionStart;
		const selectionEnd = (event.target as HTMLTextAreaElement).selectionEnd;
		const value = (event.target as HTMLTextAreaElement).value;

		text =
			value.slice(0, selectionStart) +
			value.slice(selectionStart, selectionEnd).toUpperCase() +
			value.slice(selectionEnd);

		tick().then(() => {
			(event.target as HTMLTextAreaElement).selectionStart = selectionStart;
			(event.target as HTMLTextAreaElement).selectionEnd = selectionEnd;
		});
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
		<button
			slot="footer"
			let:didAgree={closable}
			disabled={!closable}
			on:click={() => (showModal = false)}>Complete</button
		>
	</Modal>
{/if}

<textarea rows="5" on:keydown={transformText}>{text}</textarea>
