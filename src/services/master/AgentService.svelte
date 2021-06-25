<script context='module'>
	import { djrfetch } from '$services/FetchWrapper.svelte';

	export async function agentGetAll() {
		return djrfetch({ 'command': 'LIST_AGEN' });
	}

	export async function agentGetDetailById(id) {
		return djrfetch(
			{
				command: 'DETAIL_AGEN',
				idagen: id
			}
		);
	}

	export async function agentDeleteById(id) {
		return djrfetch(
			{
				command: 'DELETE_AGEN',
				idagen: id,
				deleteby: 'TODO'
			}
		);
	}

	export async function agentEditById(id, data) {
		console.log(
			{
				command: 'UPDATE_AGEN',
				idagen: id,
				updateby: 'TODO',
				...data
			}
		);
		return djrfetch(
			{
				command: 'UPDATE_AGEN',
				idagen: id,
				updateby: 'TODO',
				...data
			}
		);
	}
</script>