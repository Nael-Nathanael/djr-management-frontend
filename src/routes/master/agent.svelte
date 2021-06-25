<script>
	import AgentTable from '../../components/master/agent/AgentTable.svelte';
	let toggle;
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
			<button class='btn btn-primary' on:click={toggle} type='button'>
				<i class='fa fa-plus'></i> Add Agent
			</button>
		</div>
		<div class='card-body'>
			<AgentTable />
		</div>
	</div>
</div>