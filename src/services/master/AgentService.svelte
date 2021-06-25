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
		return djrfetch(
			{
				command: 'UPDATE_AGEN',
				idagen: id,
				updateby: 'TODO',
				...data
			}
		);
	}

	export async function agentAdd(data) {
		return djrfetch(
			{
				command: 'ADD_AGEN',
				crateby: 'TODO',
				...data
			}
		);
	}
</script>