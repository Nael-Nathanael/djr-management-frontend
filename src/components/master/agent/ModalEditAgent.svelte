<script>
	import {
		Modal
	} from 'sveltestrap/src';
	import { agentGetDetailById, agentEditById } from '$services/master/AgentService.svelte';

	export let idToEdit;
	export let requireUpdate;

	let idagen;
	let nama;
	let nomortelp;
	let email;
	let alamat;
	let kota;

	let isOpen = false;

	$: if (idToEdit) {
		fetchDetailAgen(idToEdit);
	}

	async function fetchDetailAgen(id) {
		const {
			email: email1,
			idagen: idagen1,
			nama: nama1,
			nomortelp: nomortelp1,
			alamat: alamat1,
			kota: kota1,
			responsecode
		} = await agentGetDetailById(id);

		if (responsecode === '0000') {
			idagen = idagen1;
			nama = nama1;
			nomortelp = nomortelp1;
			email = email1;
			alamat = alamat1;
			kota = kota1;
			toggle();
		}

		idToEdit = null;
	}

	let toggle = () => isOpen = !isOpen;

	async function submitChanges(event) {
		event.preventDefault();

		const updateresponse = await agentEditById(idagen,
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

<Modal centered header='Edit Agent' {isOpen} {toggle}>
	<form class='modal-body' on:submit={submitChanges}>
		<div class='form-group mb-2'>
			<label class='form-label' for='idagen'>ID</label>
			<input class='form-control' id='idagen' readonly type='text' value='{idagen}'>
		</div>
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
