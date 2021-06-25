<script>
	import AgentTable from '../../components/master/agent/AgentTable.svelte';
	import AddButton from '../../components/buttons/AddButton.svelte';
	import ModalAddAgent from '../../components/master/agent/ModalAddAgent.svelte';

	let isOpen = false;
	let requireUpdate = false;
</script>

<svelte:head>
	<title>Agent - DJR Management</title>
</svelte:head>

<div class='container'>
	<div class='card shadow-sm'>
		<div class='card-header d-flex justify-content-between align-items-center'>
			<h2 class='m-0'>
				Agent List
			</h2>
			<AddButton on:click={() => isOpen = true} things='Agent' />
		</div>
		<div class='card-body'>
			<AgentTable bind:requireUpdate />
		</div>
	</div>
</div>

<ModalAddAgent bind:isOpen bind:requireUpdate />