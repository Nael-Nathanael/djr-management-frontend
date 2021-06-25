<script context='module'>
	const URL = 'http://165.22.61.192:9911';

	export async function djrfetch(data) {
		const fetchInfo = {
			method: 'POST',
			body: JSON.stringify(data)
		};

		return await fetch(URL, fetchInfo).then((x) => x.json());
	}
</script>