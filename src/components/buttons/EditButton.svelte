<script>
	import { Tooltip } from 'sveltestrap/src';

	export let id = "#";
</script>

<button class='btn btn-warning text-white djr-fab' id='btn-edit-{id}' on:click type='button'>
	<i class='fa fa-pen'></i>
</button>
<Tooltip placement='top' target={`btn-edit-${id}`}>Detail</Tooltip>