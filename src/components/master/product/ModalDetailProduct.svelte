<script>
	import {
		Modal
	} from 'sveltestrap/src';
	import { productGetDetailById } from '$services/master/ProductService.svelte';

	export let idToShowDetail = false;

	let kodeproduk;
	let warna;
	let tipe;
	let ukuran;
	let harga;

	let isOpen = false;

	$: if (idToShowDetail) {
		showDetailProduct(idToShowDetail);
	}

	async function showDetailProduct(id) {
		const {
			kodeproduk: kodeproduk1,
			warna: warna1,
			tipe: tipe1,
			ukuran: ukuran1,
			harga: harga1,
			responsecode
		} = await productGetDetailById(id);

		if (responsecode === '0000') {
			kodeproduk = kodeproduk1;
			warna = warna1;
			tipe = tipe1;
			ukuran = ukuran1;
			harga = harga1;
			toggle();
		}

		idToShowDetail = null;
	}

	let toggle = () => isOpen = !isOpen;
</script>

<Modal body centered header='Product Detail' {isOpen} {toggle}>
	<table>
		<tr>
			<td>ID</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{kodeproduk}</td>
		</tr>
		<tr>
			<td>Color code</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{warna}</td>
		</tr>
		<tr>
			<td>Tipe</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{tipe}</td>
		</tr>
		<tr>
			<td>Size</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{ukuran}</td>
		</tr>
		<tr>
			<td>Price</td>
			<td class='ps-3 pe-2'>:</td>
			<td>{harga}</td>
		</tr>
	</table>
</Modal>
