<script>
	import { Modal, Tooltip } from 'sveltestrap/src';
	import { onMount } from 'svelte';

	const url = 'http://165.22.61.192:9911';

	let isOpen = false;
	const toggle = () => isOpen = !isOpen;

	let daftarAgen = [];

	let detail = {};

	$: console.log(detail);

	onMount(fetchDaftarAgen);

	async function fetchDaftarAgen() {
		const fetchInfo = {
			method: 'POST',
			body: JSON.stringify({ 'command': 'LIST_AGEN' })
		};

		const { listagen, responsecode } = await fetch(url, fetchInfo).then((x) => x.json());

		if (responsecode === '0000') {
			daftarAgen = listagen;
		} else if (responsecode === '0099') {
			alert('error pada backend sistem');
		}
	}

	async function showDetailAgen(id) {
		const fetchInfo = {
			method: 'POST',
			body: JSON.stringify({
				command: 'DETAIL_AGEN',
				idagen: id
			})
		};

		const detailresponse = await fetch(url, fetchInfo).then((x) => x.json());

		if (detailresponse.responsecode === '0000') {
			detail = detailresponse;
			toggle();
		} else if (detailresponse.responsecode === '0099') {
			alert('error pada backend sistem');
		}

		'DETAIL_AGEN';
		'bacco@example.com';
		'DJRAGN21060001';
		'Detail Data Agen';
		'BACCO';
		'08xxxxxx';
		'0000';
	}

</script>

<div class='container'>
	<div class='card shadow-sm'>
		<div class='card-header d-flex justify-content-between align-items-center'>
			<h2 class='m-0'>
				Agent List
			</h2>
			<button class='btn btn-primary' on:click={toggle} type='button'>
				<i class='fa fa-plus'></i> Add Agent
			</button>
		</div>
		<div class='card-body'>
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
								<button class='btn btn-primary djr-fab' type='button' id='btn-view-{idagen}'
												on:click={() => showDetailAgen(idagen)}>
									<i class='fa fa-eye'></i>
								</button>
								<Tooltip target={`btn-view-${idagen}`} placement='top'>View Detail</Tooltip>

								<button class='btn btn-warning text-white djr-fab' type='button' id='btn-edit-{idagen}'>
									<i class='fa fa-pen'></i>
								</button>
								<Tooltip target={`btn-edit-${idagen}`} placement='top'>Edit</Tooltip>

								<button class='btn btn-danger text-white djr-fab' type='button' id='btn-delete-{idagen}'>
									<i class='fa fa-trash'></i>
								</button>
								<Tooltip target={`btn-delete-${idagen}`} placement='top'>Delete</Tooltip>
							</div>
						</td>
					</tr>
				{/each}

				</tbody>
			</table>
		</div>
	</div>
</div>

<Modal body centered header='Detail Agen' {isOpen} {toggle}>
	<table>
		<tr>
			<td>ID</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{detail.idagen}</td>
		</tr>
		<tr>
			<td>Nama</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{detail.nama}</td>
		</tr>
		<tr>
			<td>Nomor Telepon</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{detail.nomortelp}</td>
		</tr>
		<tr>
			<td>Email</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{detail.email}</td>
		</tr>
	</table>
</Modal>