<script>
	import ProductTable from '$components/master/product/ProductTable.svelte';
	import AddButton from '$components/buttons/AddButton.svelte';
	import ModalAddProduct from '$components/master/product/ModalAddProduct.svelte';

	let isOpen = false;
	let requireUpdate = false;
</script>

<svelte:head>
	<title>Product - DJR Management</title>
</svelte:head>

<div class='container'>
	<div class='card shadow-sm'>
		<div class='card-header d-flex justify-content-between align-items-center'>
			<h2 class='m-0'>
				Product List
			</h2>
			<AddButton on:click={() => isOpen = true} things='Product' />
		</div>
		<div class='card-body'>
			<ProductTable bind:requireUpdate />
		</div>
	</div>
</div>

<ModalAddProduct bind:isOpen bind:requireUpdate />