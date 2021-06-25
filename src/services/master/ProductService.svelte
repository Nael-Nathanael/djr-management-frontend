<script context='module'>
	import { djrfetch } from '$services/FetchWrapper.svelte';

	export async function productGetAll() {
		return djrfetch({ 'command': 'LIST_PRODUCT' });
	}

	export async function productGetDetailById(id) {
		return djrfetch(
			{
				command: 'DETAIL_PRODUCT',
				kodeproduk: id
			}
		);
	}

	export async function productDeleteById(id) {
		return djrfetch(
			{
				command: 'DELETE_PRODUCT',
				kodeproduk: id,
				deleteby: 'TODO'
			}
		);
	}

	export async function productEditById(id, data) {
		return djrfetch(
			{
				command: 'UPDATE_PRODUCT',
				kodeproduk: id,
				updateby: 'TODO',
				...data
			}
		);
	}

	export async function productAdd(data) {
		return djrfetch(
			{
				command: 'ADD_PRODUCT',
				createby: 'TODO',
				...data
			}
		);
	}
</script>