<script>
	import Swal from 'sweetalert2';
	import { onMount } from 'svelte';
	import 'sweetalert2/dist/sweetalert2.css';
	import { agentGetAll, agentDeleteById } from '$services/master/AgentService.svelte';

	import DetailButton from '../../buttons/DetailButton.svelte';
	import DeleteButton from '../../buttons/DeleteButton.svelte';
	import EditButton from '../../buttons/EditButton.svelte';
	import ModalDetailAgent from './ModalDetailAgent.svelte';
	import ModalEditAgent from './ModalEditAgent.svelte';

	let daftarAgen = [];
	let idToShowDetail;
	let idToEdit;

	let requireUpdate = false;

	$: if (requireUpdate) {
		fetchDaftarAgen();
	}

	onMount(fetchDaftarAgen);

	async function fetchDaftarAgen() {
		const { listagen, responsecode } = await agentGetAll();

		if (responsecode === '0000') {
			daftarAgen = listagen;
		}
	}

	function confirmDeleteAgen(id) {
		Swal.fire({
			title: 'Are you sure?',
			text: 'You won\'t be able to revert this!',
			icon: 'warning',
			confirmButtonColor: '#dc3545',
			confirmButtonText: 'Yes, Delete Agent',
			showCancelButton: true
		}).then((result) => {
			if (result.isConfirmed) {
				deleteAgen(id);
			}
		});
	}

	async function deleteAgen(id) {
		const { message, responsecode } = await agentDeleteById(id);
		if (responsecode === '0000') {
			await Swal.fire('Success!', message, 'success');
			await fetchDaftarAgen();
		} else if (responsecode === '0099') {
			alert('error pada backend sistem');
		}
	}
</script>

<table class='table table-hover'>
	<thead>
	<tr>
		<th>No</th>
		<th>ID</th>
		<th>Name</th>
		<th>Phone Number</th>
		<th>Email</th>
		<th class='text-center'>Action</th>
	</tr>
	</thead>
	<tbody>
	{#each daftarAgen as { idagen, nama, nomortelp, email }, index}
		<tr>
			<td>{index + 1}</td>
			<td>
				{idagen}
			</td>
			<td>
				{nama}
			</td>
			<td>
				{nomortelp}
			</td>
			<td>
				{email}
			</td>
			<td>
				<div class='d-flex justify-content-center align-items-center'>
					<DetailButton bind:id={idagen} on:click={() => idToShowDetail = idagen} />
					<EditButton bind:id={idagen} on:click={() => idToEdit = idagen} />
					<DeleteButton bind:id={idagen} on:click={() => confirmDeleteAgen(idagen)} />
				</div>
			</td>
		</tr>
	{/each}
	</tbody>
</table>

<ModalDetailAgent
	bind:idToShowDetail
/>

<ModalEditAgent
	bind:idToEdit
	bind:requireUpdate
/>