<script>
	import {
		Modal
	} from 'sveltestrap/src';
	import { productAdd } from '$services/master/ProductService.svelte';

	export let isOpen = false;

	let kodewarna;
	let tipe;
	let ukuran;
	let harga;

	let toggle = () => isOpen = !isOpen;
	export let requireUpdate = false;

	async function submitAdd(event) {
		event.preventDefault();
		const updateresponse = await productAdd(
			{
				kodewarna: kodewarna,
				tipe: tipe,
				ukuran: ukuran,
				harga: harga
			}
		);

		console.log(updateresponse);

		if (updateresponse.responsecode === '0000') {
			requireUpdate = true;
			toggle();
		}
	}
</script>

<Modal centered header='Add Product' {isOpen} {toggle}>
	<form class='modal-body' on:submit={submitAdd}>
		<div class='form-group mb-2'>
			<label class='form-label' for='kodewarna'>Color code</label>
			<input bind:value='{kodewarna}' class='form-control' id='kodewarna' required type='text'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='tipe'>Tipe</label>
			<input bind:value='{tipe}' class='form-control' id='tipe' required type='text'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='ukuran'>Size</label>
			<input bind:value='{ukuran}' class='form-control' id='ukuran' required type='text'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='harga'>Price</label>
			<input bind:value='{harga}' class='form-control' id='harga' required type='text'>
		</div>
		<div class='w-100 d-flex justify-content-end'>
			<button class='btn btn-primary' type='submit'>Submit</button>
		</div>
	</form>

</Modal>
