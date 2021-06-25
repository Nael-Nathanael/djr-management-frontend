<script>
	import {
		Modal
	} from 'sveltestrap/src';
	import { agentGetDetailById } from '$services/master/AgentService.svelte';

	export let idToShowDetail;

	let idagen;
	let nama;
	let nomortelp;
	let email;

	let isOpen = false;

	$: if (idToShowDetail) {
		showDetailAgen(idToShowDetail);
	}

	async function showDetailAgen(id) {
		const {
			email: email1,
			idagen: idagen1,
			nama: nama1,
			nomortelp: nomortelp1,
			responsecode
		} = await agentGetDetailById(id);

		if (responsecode === '0000') {
			idagen = idagen1;
			nama = nama1;
			nomortelp = nomortelp1;
			email = email1;
			toggle();
		}

		idToShowDetail = null;
	}

	let toggle = () => isOpen = !isOpen;
</script>

<Modal body centered header='Agent Detail' {isOpen} {toggle}>
	<table>
		<tr>
			<td>ID</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{idagen}</td>
		</tr>
		<tr>
			<td>Name</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{nama}</td>
		</tr>
		<tr>
			<td>Phone number</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{nomortelp}</td>
		</tr>
		<tr>
			<td>Email</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{email}</td>
		</tr>
	</table>
</Modal>
