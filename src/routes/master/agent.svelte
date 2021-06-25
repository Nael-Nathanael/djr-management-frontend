<script>
	import { Modal } from 'sveltestrap/src';
	import { onMount } from 'svelte';

	let isOpen = false;
	const toggle = () => isOpen = !isOpen;

	onMount(async () => {
		const url = 'https://165.22.61.192:9911';
		const body = {
			command: 'LIST_AGEN'
		};

		const headers = {
			'Content-Type': 'application/json',
		};

		const fetchInfo = {
			method: 'POST',
			headers: headers,
			body: JSON.stringify(body)
		};

		fetch(url, fetchInfo)
			.then((response) => {
				console.log(response);
			})
			.catch((error) => {
				console.log(error);
			});

	});
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
		</div>
	</div>
</div>

<Modal body centered header='Hello World!' {isOpen} {toggle}>
	<p>
		There's a song that we're singing. Come on
	</p>
	<img
		alt='Come on Get Happy'
		class='img-fluid'
		src='https://i.ytimg.com/vi/NUJIRujygvY/hqdefault.jpg' />
</Modal>