<script>
	import {
		Modal
	} from 'sveltestrap/src';
	import { productGetDetailById, productEditById } from '$services/master/ProductService.svelte';

	export let idToEdit = false;
	export let requireUpdate;

	let kodeproduk;
	let warna;
	let tipe;
	let ukuran;
	let harga;

	let isOpen = false;

	$: if (idToEdit) {
		fetchDetailAgen(idToEdit);
	}

	async function fetchDetailAgen(id) {
		const {
			kodeproduk: kodeproduk1,
			warna: warna1,
			tipe: tipe1,
			ukuran: ukuran1,
			harga: harga1,
			responsecode
		} = await productGetDetailById(id);

		if (responsecode === '0000') {
			kodeproduk = kodeproduk1;
			warna = warna1;
			tipe = tipe1;
			ukuran = ukuran1;
			harga = harga1;
			toggle();
		}

		idToEdit = null;
	}

	let toggle = () => isOpen = !isOpen;

	async function submitChanges(event) {
		event.preventDefault();

		const updateresponse = await productEditById(kodeproduk,
			{
				kodewarna: warna,
				tipe: tipe,
				ukuran: ukuran,
				harga: harga
			}
		);

		if (updateresponse.responsecode === '0000') {
			requireUpdate = true;
			toggle();
		}
	}
</script>

<Modal centered header='Edit Agent' {isOpen} {toggle}>
	<form class='modal-body' on:submit={submitChanges}>
		<div class='form-group mb-2'>
			<label class='form-label' for='kodeproduk'>ID</label>
			<input class='form-control' id='kodeproduk' readonly type='text' value='{kodeproduk}'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='warna'>Color Code</label>
			<input bind:value='{warna}' class='form-control' id='warna' required type='text'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='tipe'>Type</label>
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
