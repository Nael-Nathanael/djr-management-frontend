<script>
	import { Tooltip } from 'sveltestrap/src';

	export let id = "#";
</script>

<button class='btn btn-primary djr-fab' id='btn-view-{id}' on:click type='button'>
	<i class='fa fa-eye'></i>
</button>
<Tooltip placement='top' target={`btn-view-${id}`}>Detail</Tooltip>