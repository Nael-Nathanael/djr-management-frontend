<script>
	import {
		Modal
	} from 'sveltestrap/src';
	import { agentAdd } from '$services/master/AgentService.svelte';

	export let isOpen = false;

	let nama;
	let nomortelp;
	let email;
	let alamat;
	let kota;

	let toggle = () => isOpen = !isOpen;
	export let requireUpdate = false;

	async function submitAdd(event) {
		event.preventDefault();

		const updateresponse = await agentAdd(
			{
				namaagen: nama,
				nomortelp: nomortelp,
				email: email,
				alamat: alamat,
				kota: kota
			}
		);

		if (updateresponse.responsecode === '0000') {
			requireUpdate = true;
			toggle();
		}
	}
</script>

<Modal centered header='Add Agent' {isOpen} {toggle}>
	<form class='modal-body' on:submit={submitAdd}>
		<div class='form-group mb-2'>
			<label class='form-label' for='nama'>Name</label>
			<input bind:value='{nama}' class='form-control' id='nama' required type='text'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='nomortelp'>Phone Number</label>
			<input bind:value='{nomortelp}' class='form-control' id='nomortelp' required type='text'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='email'>Email</label>
			<input bind:value='{email}' class='form-control' id='email' required type='text'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='alamat'>Alamat</label>
			<input bind:value='{alamat}' class='form-control' id='alamat' required type='text'>
		</div>
		<div class='form-group mb-2'>
			<label class='form-label' for='kota'>Kota</label>
			<input bind:value='{kota}' class='form-control' id='kota' required type='text'>
		</div>
		<div class='w-100 d-flex justify-content-end'>
			<button class='btn btn-primary' type='submit'>Submit</button>
		</div>
	</form>

</Modal>
