<script>
	import {
		Button,
		Card,
		CardBody,
		CardHeader,
		TabContent,
		TabPane,
	} from "sveltestrap";
	import Modal from "../components/Modal.svelte";
	import Tablekeranjangkombinasi from "../permainan/Tablekeranjangkombinasi.svelte";
	import Loader from "../components/Loader.svelte";
	import { createEventDispatcher } from "svelte";

	export let idcomppasaran = "";
	export let idtrxkeluaran = "";
	export let client_token = "";
	export let client_company = "";
	export let client_username = "";
	export let client_ipaddress = "";
	export let client_device = "";
	export let client_timezone = "";
	export let pasaran_code = "";
	export let pasaran_name = "";
	export let pasaran_periode = 0;
	export let permainan_title = "COLOK";
	let keranjang = [];
	let css_loader = "display:none;";
	let nomor_global = 0;
	let totalkeranjang = 0;
	let group_btn_beli = false;
	let record = "";
	let temp_bulk_error = "";
	let flag_fulldiskon = "DISC"
	let min_bet = 0;
	let max_bet = 0;
	let win_bet = 0;
	let diskon_bet = 0;

	let limit_total = 0;

	let count_line_macaukombinasi = 0;
	let count_line_standart = 0;

	let db_formkombinasi = 0;
	let db_formkombinasi_dasar = 0;

	let dispatch = createEventDispatcher();

	async function inittogel_432d(e) {
		const res = await fetch("/api/inittogel_432d", {
			method: "POST",
			headers: {
				"Content-Type": "application/json",
			},
			body: JSON.stringify({
				company: client_company,
				pasaran_code: pasaran_code,
				permainan: e,
			}),
		});
		group_btn_beli = true;
		const json = await res.json();
		record = json.record;

		for (var i = 0; i < record.length; i++) {
			min_bet = parseInt(record[i]["min_bet"]);
			max_bet = parseInt(record[i]["max_bet"]);
			win_bet = parseFloat(record[i]["win_bet"]);
			diskon_bet = parseFloat(record[i]["diskon_bet"]);
			limit_total = parseInt(record[i]["limit_total"]);
		}
	}
	async function savetransaksi() {
		if (client_device == "WEBSITE") {
			css_loader =
				"position:absolute;z-index: 1000;left: 50%;top: 35%;display:inline;";
		} else {
			css_loader =
				"position:absolute;z-index: 1000;left: 0%;top: 35%;display:inline;";
		}
		group_btn_beli = false;
		const res = await fetch("/api/savetransaksi", {
			method: "POST",
			headers: {
				"Content-Type": "application/json",
			},
			body: JSON.stringify({
				pasaran_idtransaction: idtrxkeluaran,
				pasaran_idcomp: idcomppasaran,
				pasaran_code: pasaran_code,
				pasaran_periode: pasaran_periode,
				token: client_token,
				company: client_company,
				username: client_username,
				ipaddress: client_ipaddress,
				devicemember: client_device,
				timezone: client_timezone,
				total: totalkeranjang,
				data: keranjang,
			}),
		});
		const json = await res.json();
		if (json.status == "200") {
			css_loader = "display:none;";
			alert(
				"Data telah berhasil disimpan, Total belanja : " +
					new Intl.NumberFormat().format(totalkeranjang)
			);
			dispatch("handleInvoice", "call");
			reset();
		} else {
			css_loader = "display:none;";
			if (json.status == "500" || json.status == "404") {
				group_btn_beli = true;
				alert(json.message);
			}
		}
	}
	function reset() {
		keranjang = [];
		group_btn_beli = true;
		totalkeranjang = 0;
		count_line_macaukombinasi = 0;
		count_line_standart = 0;
	}
	inittogel_432d("macaukombinasi");
	function addKeranjang(
		nomor,
		game,
		bet,
		diskon_percen,diskon,bayar,win,
		kei_percen,kei,tipetoto) {
		let total_data = keranjang.length;
		let flag_data = false;
		for (var i = 0; i < total_data; i++) {
			switch (game) {
				case "MACAU_KOMBINASI":
					if (nomor == keranjang[i].nomor.toString()) {
						let maxtotal_bayarmacaukombinasi = 0;
						for (var j = 0; j < keranjang.length; j++) {
							if ("50_50_UMUM" == keranjang[j].permainan) {
								if (
									parseInt(nomor) ==
									parseInt(keranjang[j].nomor)
								) {
									maxtotal_bayarmacaukombinasi =
										parseInt(maxtotal_bayarmacaukombinasi) +
										(parseInt(keranjang[j].bet) +
											parseInt(bet));
								}
							}
						}
						if (
							parseInt(limittotal_bet_macaukombinasi) <
							parseInt(maxtotal_bayarmacaukombinasi)
						) {
							temp_bulk_error +=
								"Nomor ini : " +
								nomor +
								" sudah melebihi LIMIT TOTAL MACAU KOMBINASI<br />";
							flag_data = true;
						}
					}
					break;
			}
		}

		if (flag_data == false) {
			nomor_global = nomor_global + 1;
			const data = {
				id: nomor_global,
				nomor,
				permainan: game,
				bet,
				diskon,
				diskonpercen: diskon_percen,
				bayar,
				win,
				kei,
				kei_percen,tipetoto
			};
			keranjang = [data, ...keranjang];
			count_keranjang();
		}
	}
	const removekeranjang = (e) => {
		keranjang = keranjang.filter(
			(keranjang) => keranjang.id != e.detail.idkeranjang
		);
		totalkeranjang = totalkeranjang - e.detail.bayar;
		count_keranjang();
	};
	const removekeranjangall = (e) => {
		if (keranjang.length > 0) {
			reset();
			count_keranjang();
		} else {
			alert("Tidak ada list transaksi");
		}
	};
	const handleSave = (e) => {
		if (keranjang.length > 0) {
			savetransaksi();
		} else {
			alert("Tidak ada list transaksi");
		}
	};
	function count_keranjang() {
		let count_umum = 0;
		let count_kombinasi = 0;
		for (let i = 0; i < keranjang.length; i++) {
			switch (keranjang[i].permainan.toString()) {
				case "MACAU_KOMBINASI":
					count_kombinasi = count_kombinasi + 1;
					break;
			}
		}
		count_line_macaukombinasi = count_kombinasi + db_formkombinasi;
		count_line_standart = count_umum + db_formkombinasi_dasar;
	}

	//KOMBINASI - INIT FORM
	let select_kombinasi_1 = "";
	let select_kombinasi_1_input;
	let select_kombinasi_2 = "";
	let select_kombinasi_2_input;
	let select_kombinasi_3 = "";
	let select_kombinasi_3_input;
	let bet_kombinasi = "";

	function form_clear(e) {
		switch (e) {
			case "macaukombinasi":
				select_kombinasi_1 = "";
				select_kombinasi_2 = "";
				select_kombinasi_3 = "";
				select_kombinasi_1_input.focus();
				bet_kombinasi = 0;
				break;
		}
	}

	function formkombinasi_add() {
		let flag = true;
		let nomor = select_kombinasi_1;
		let nomor2 = select_kombinasi_2;
		let nomor3 = select_kombinasi_3;
		let bet = bet_kombinasi;
		let diskon = 0;
		let diskonpercen = 0;
		let win = win_bet;
		let kei = 0;
		let keipersen = 0;
		let bayar = 0;
		let nmgame = "MACAU_KOMBINASI";

		if (nomor == "") {
			select_kombinasi_1_input.focus();
			flag = false;
			alert("Tebak tidak boleh kosong");
		}
		if (nomor2 == "") {
			select_kombinasi_2_input.focus();
			flag = false;
			alert("Tebak tidak boleh kosong");
		}
		if (nomor3 == "") {
			select_kombinasi_3_input.focus();
			flag = false;
			alert("Tebak tidak boleh kosong");
		}
		if (bet == "") {
			flag = false;
			alert("Amount tidak boleh kosong");
		}
		if (parseInt(bet) < parseInt(min_bet)) {
			bet_kombinasi = min_bet;
			flag = false;
			alert("Minimal Bet : " + min_bet);
		}
		if (parseInt(bet) > parseInt(max_bet)) {
			bet_kombinasi = max_bet;
			flag = false;
			alert(" Maximal Bet : " + max_bet);
		}
		if (flag == true) {
			diskon = bet * diskon_bet;
			diskonpercen = diskon_bet;
			win = win_bet;
			bayar = parseInt(bet) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;

			addKeranjang(
				nomor + "_" + nomor2 + "_" + nomor3,
				nmgame,
				bet_kombinasi,
				diskonpercen,
				diskon,
				bayar,
				win,
				keipersen,
				kei,flag_fulldiskon
			);
			form_clear("macaukombinasi");
		}
	}
	const handleTambah = (e) => {
		switch (e) {
			case "macaukombinasi":
				if (select_kombinasi_1 == "" && select_kombinasi_2 == "" && select_kombinasi_3 == "" && parseInt(bet_kombinasi) < min_bet) {
					select_kombinasi_1_input.focus();
				} else {
					formkombinasi_add();
				}
				break;
		}
	};

	const handleKeyboard_number = (e) => {
		let numbera;
		for (let i = 0; i < bet_kombinasi.length; i++) {
			numbera = parseInt(bet_kombinasi[i]);
			if (isNaN(numbera)) {
				bet_kombinasi = "";
			}
		}
	};
	const handleKeyboard_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			formkombinasi_add();
		}
	};
</script>

<Loader cssstyle={css_loader} />
{#if client_device == "WEBSITE"}
	<Card color="dark" style="border:1px solid #262424;">
		<CardHeader style="background:#323030;border-bottom:1px solid #333;border-top: 0 solid #333;">
			<div class="float-end">
				<div style="color:white;text-align:right;font-size:13px;font-weight:bold;">
					{pasaran_name}
				</div>
			</div>
			<h1 style="padding:0px;margin:0px;color:white;font-size:15px;">
				{permainan_title}<br />
				PERIODE : {pasaran_periode + " - " + pasaran_code}
			</h1>
		</CardHeader>
		<CardBody style="background:#121212;padding:0px;margin:0px;">
			<div style="margin:5px;">
				<table class="table" style="background:none;width:100%;">
					<tr>
						<td
							width="25%"
							NOWRAP
							style="padding-right:10px;vertical-align: center;"
						>
							<span style="color:#8a8a8a;">TEBAK</span>
							<select
								bind:value={select_kombinasi_1}
								bind:this={select_kombinasi_1_input}
								style="border:none;background:#303030;color:white;"
								class="form-control"
							>
								<option value="">--Pilih--</option>
								<option value="BELAKANG">BELAKANG</option>
								<option value="TENGAH">TENGAH</option>
								<option value="DEPAN">DEPAN</option>
							</select>
							<span
								class="help-block"
								style="text-align:right;font-size:12px;"
							/>
						</td>
						<td
							width="25%"
							NOWRAP
							style="padding-right:10px;vertical-align: center;"
						>
							<span style="color:#8a8a8a;">TEBAK</span>
							<select
								bind:value={select_kombinasi_2}
								bind:this={select_kombinasi_2_input}
								style="border:none;background:#303030;color:white;"
								class="form-control"
							>
								<option value="">--Pilih--</option>
								<option value="BESAR">BESAR</option>
								<option value="KECIL">KECIL</option>
							</select>
							<span
								class="help-block"
								style="text-align:right;font-size:12px;"
							/>
						</td>
						<td
							width="25%"
							NOWRAP
							style="padding-right:10px;vertical-align: center;"
						>
							<span style="color:#8a8a8a;">TEBAK</span>
							<select
								bind:value={select_kombinasi_3}
								bind:this={select_kombinasi_3_input}
								style="border:none;background:#303030;color:white;"
								class="form-control"
							>
								<option value="">--Pilih--</option>
								<option value="GENAP">GENAP</option>
								<option value="GANJIL">GANJIL</option>
							</select>
							<span
								class="help-block"
								style="text-align:right;font-size:12px;"
							/>
						</td>
						<td
							width="*"
							NOWRAP
							style="padding-right:10px;vertical-align: center;text-align:right;"
						>
							<span style="color:#8a8a8a;"
								>Bet (min : {new Intl.NumberFormat().format(
									min_bet
								)} dan max : {new Intl.NumberFormat().format(
									max_bet
								)})</span
							>
							<input
								bind:value={bet_kombinasi}
								on:keyup={handleKeyboard_number}
								on:keypress={handleKeyboard_checkenter}
								type="text"
								class="form-control"
								placeholder="Bet"
								style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
								minlength="3"
								maxlength="7"
								tab_index="0"
							/>
							<span
								style="text-align:right;font-size:12px;color:#8a8a8a;"
								>{new Intl.NumberFormat().format(
									bet_kombinasi
								)}</span
							>
						</td>
						<td width="20%" NOWRAP style="vertical-align: center;">
							<Button
								id="btn2"
								on:click={() => {
									handleTambah("macaukombinasi");
								}}>TAMBAH</Button
							>
						</td>
					</tr>
				</table>
			</div>
		</CardBody>
	</Card>
{:else}
	<Card color="dark" style="border:1px solid #262424;margin:0px;padding:0px;">
		<CardHeader
			style="background:#323030;border-bottom:1px solid #333;border-top: 0 solid #333;"
		>
			<div class="float-end">
				<div
					style="color:white;text-align:right;font-size:12px;font-weight:bold;"
				>
					{pasaran_name}
				</div>
			</div>
			<h1 style="padding:0px;margin:0px;color:white;font-size:12px;">
				{permainan_title}<br />
				PERIODE : {pasaran_periode + " - " + pasaran_code}
			</h1>
		</CardHeader>
		<CardBody style="background:#121212;padding:0px;margin:0px;">
			<div style="margin:5px;">
				<table class="table" style="background:none;width:100%;">
					<tr>
						<td
							width="25%"
							NOWRAP
							style="padding-right:10px;vertical-align: center;"
						>
							<span style="color:#8a8a8a;">TEBAK</span>
							<select
								bind:value={select_kombinasi_1}
								bind:this={select_kombinasi_1_input}
								style="border:none;background:#303030;color:white;"
								class="form-control"
							>
								<option value="">--Pilih--</option>
								<option value="BELAKANG">BELAKANG</option>
								<option value="TENGAH">TENGAH</option>
								<option value="DEPAN">DEPAN</option>
							</select>
							<span
								class="help-block"
								style="text-align:right;font-size:12px;"
							/>
						</td>
						<td
							width="25%"
							NOWRAP
							style="padding-right:10px;vertical-align: center;"
						>
							<span style="color:#8a8a8a;">TEBAK</span>
							<select
								bind:value={select_kombinasi_2}
								bind:this={select_kombinasi_2_input}
								style="border:none;background:#303030;color:white;"
								class="form-control"
							>
								<option value="">--Pilih--</option>
								<option value="BESAR">BESAR</option>
								<option value="KECIL">KECIL</option>
							</select>
							<span
								class="help-block"
								style="text-align:right;font-size:12px;"
							/>
						</td>
						<td
							width="25%"
							NOWRAP
							style="padding-right:10px;vertical-align: center;"
						>
							<span style="color:#8a8a8a;">TEBAK</span>
							<select
								bind:value={select_kombinasi_3}
								bind:this={select_kombinasi_3_input}
								style="border:none;background:#303030;color:white;"
								class="form-control"
							>
								<option value="">--Pilih--</option>
								<option value="GENAP">GENAP</option>
								<option value="GANJIL">GANJIL</option>
							</select>
							<span
								class="help-block"
								style="text-align:right;font-size:12px;"
							/>
						</td>
					</tr>
					<tr>
						<td
							colspan="3"
							NOWRAP
							style="padding-right:10px;vertical-align: center;text-align:right;"
						>
							<span style="color:#8a8a8a;"
								>Bet (min : {new Intl.NumberFormat().format(
									min_bet
								)} dan max : {new Intl.NumberFormat().format(
									max_bet
								)})</span
							>
							<input
								bind:value={bet_kombinasi}
								on:keyup={handleKeyboard_number}
								on:keypress={handleKeyboard_checkenter}
								type="text"
								class="form-control"
								placeholder="Bet"
								style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
								minlength="3"
								maxlength="7"
								tab_index="0"
							/>
							<span
								style="text-align:right;font-size:12px;color:#8a8a8a;"
								>{new Intl.NumberFormat().format(
									bet_kombinasi
								)}</span
							>
						</td>
					</tr>
				</table>
				<Button
					block
					id="btn2"
					on:click={() => {
						handleTambah("macaukombinasi");
					}}>TAMBAH</Button
				>
			</div>
		</CardBody>
	</Card>
{/if}
<Modal modal_id={"modalError"} modal_size={"modal-dialog-centered"}>
	<slot:template slot="header">
		<div class="float-end">
			<img
				style="cursor:pointer;"
				data-bs-dismiss="modal"
				aria-label="Close"
				width="25"
				src="https://i.ibb.co/9yNF25L/outline-close-white-48dp.png"
				alt=""
			/>
		</div>
		<h5 class="modal-title" id="exampleModalLabel">ERROR</h5>
	</slot:template>
	<slot:template slot="body">
		{@html temp_bulk_error}
	</slot:template>
</Modal>
<div class="clearfix" />
<br />
<Tablekeranjangkombinasi
	on:removekeranjang={removekeranjang}
	on:removekeranjangall={removekeranjangall}
	on:handleSave={handleSave}
	{client_device}
	{group_btn_beli}
	{count_line_macaukombinasi}
	{count_line_standart}
	{keranjang}
	{totalkeranjang}
	{min_bet}
	{max_bet}
	{win_bet}
	{diskon_bet}
/>

<style>
	input,
	input::-webkit-input-placeholder {
		font-size: 13px;
		color: #8a8a8a;
	}
	input::placeholder {
		color: #8a8a8a;
	}
</style>
