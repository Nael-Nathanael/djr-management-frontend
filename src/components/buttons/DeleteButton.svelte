<script>
	import { Tooltip } from 'sveltestrap/src';

	export let id = "#";
</script>

<button class='btn btn-danger text-white djr-fab' id='btn-delete-{id}' on:click type='button'>
	<i class='fa fa-trash'></i>
</button>
<Tooltip placement='top' target={`btn-delete-${id}`}>Detail</Tooltip>