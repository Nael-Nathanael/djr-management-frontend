<script>
	import Swal from 'sweetalert2';
	import { onMount } from 'svelte';
	import 'sweetalert2/dist/sweetalert2.css';
	import { productGetAll, productDeleteById } from '$services/master/ProductService.svelte';

	import DetailButton from '../../buttons/DetailButton.svelte';
	import DeleteButton from '../../buttons/DeleteButton.svelte';
	import EditButton from '../../buttons/EditButton.svelte';
	import ModalDetailProduct from './ModalDetailProduct.svelte';
	import ModalEditProduct from './ModalEditProduct.svelte';

	let daftarProduk = [];
	let idToShowDetail;
	let idToEdit;

	export let requireUpdate = false;

	$: if (requireUpdate) {
		fetchDaftarProduk();
	}

	onMount(fetchDaftarProduk);

	async function fetchDaftarProduk() {
		const productresponse = await productGetAll();

		if (productresponse.responsecode === '0000') {
			daftarProduk = productresponse.listdata;
		}
	}

	function confirmDeleteProduk(id) {
		Swal.fire({
			title: 'Are you sure?',
			text: 'You won\'t be able to revert this!',
			icon: 'warning',
			confirmButtonColor: '#dc3545',
			confirmButtonText: 'Yes, Delete Product',
			showCancelButton: true
		}).then((result) => {
			if (result.isConfirmed) {
				deleteProduk(id);
			}
		});
	}

	async function deleteProduk(id) {
		const { message, responsecode } = await productDeleteById(id);
		if (responsecode === '0000') {
			await Swal.fire('Success!', message, 'success');
			await fetchDaftarProduk();
		} else if (responsecode === '0099') {
			alert('error pada backend sistem');
		}
	}
</script>

<table class='table table-hover'>
	<thead>
	<tr>
		<th>No</th>
		<th>Product Code</th>
		<th>Color Code</th>
		<th>Type</th>
		<th>Size</th>
		<th>Price</th>
		<th class='text-center'>Action</th>
	</tr>
	</thead>
	<tbody>
	{#each daftarProduk as { kodeproduk, warna, tipe, ukuran, harga }, index}
		<tr>
			<td>{index + 1}</td>
			<td>
				{kodeproduk}
			</td>
			<td>
				{warna}
			</td>
			<td>
				{tipe}
			</td>
			<td>
				{ukuran}
			</td>
			<td>
				{harga}
			</td>
			<td>
				<div class='d-flex justify-content-center align-items-center'>
					<DetailButton bind:id={kodeproduk} on:click={() => idToShowDetail = kodeproduk} />
					<EditButton bind:id={kodeproduk} on:click={() => idToEdit = kodeproduk} />
					<DeleteButton bind:id={kodeproduk} on:click={() => confirmDeleteProduk(kodeproduk)} />
				</div>
			</td>
		</tr>
	{/each}
	</tbody>
</table>

<ModalDetailProduct
	bind:idToShowDetail
/>

<ModalEditProduct
	bind:idToEdit
	bind:requireUpdate
/>