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
	import Tablekeranjangcolok from "../permainan/Tablekeranjangcolok.svelte";
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
	let min_bet_colokbebas = 0;
	let max_bet_colokbebas = 0;
	let disc_bet_colokbebas = 0;
	let win_bet_colokbebas = 0;
	let limittotal_bet_colokbebas = 0;
	let min_bet_colokmacau = 0;
	let max_bet_colokmacau = 0;
	let disc_bet_colokmacau = 0;
	let win_bet_colokmacau = 0;
	let win3_bet_colokmacau = 0;
	let win4_bet_colokmacau = 0;
	let limittotal_bet_colokmacau = 0;
	let min_bet_coloknaga = 0;
	let max_bet_coloknaga = 0;
	let disc_bet_coloknaga = 0;
	let win_bet_coloknaga = 0;
	let win4_bet_coloknaga = 0;
	let limittotal_bet_coloknaga = 0;
	let min_bet_colokjitu = 0;
	let max_bet_colokjitu = 0;
	let disc_bet_colokjitu = 0;
	let winas_bet_colokjitu = 0;
	let winkop_bet_colokjitu = 0;
	let winkepala_bet_colokjitu = 0;
	let winekor_bet_colokjitu = 0;
	let limittotal_bet_colokjitu = 0;

	let count_line_colokbebas = 0;
	let count_line_colokmacau = 0;
	let count_line_coloknaga = 0;
	let count_line_colokjitu = 0;

	let db_formcolok_colokbebas_count_temp = 0;
	let db_formcolok_colokmacau_count_temp = 0;
	let db_formcolok_coloknaga_count_temp = 0;
	let db_formcolok_colokjitu_count_temp = 0;

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
		min_bet_colokbebas = record[0]["min_bet"];

		for (var i = 0; i < record.length; i++) {
			min_bet_colokbebas = parseInt(record[i]["min_bet_colokbebas"]);
			max_bet_colokbebas = parseInt(record[i]["max_bet_colokbebas"]);
			disc_bet_colokbebas = parseFloat(record[i]["disc_bet_colokbebas"]);
			win_bet_colokbebas = parseFloat(record[i]["win_bet_colokbebas"]);
			limittotal_bet_colokbebas = parseInt(record[i]["limittotal_bet_colokbebas"]);
			min_bet_colokmacau = parseInt(record[i]["min_bet_colokmacau"]);
			max_bet_colokmacau = parseFloat(record[i]["max_bet_colokmacau"]);
			disc_bet_colokmacau = parseFloat(record[i]["disc_bet_colokmacau"]);
			win_bet_colokmacau = parseFloat(record[i]["win_bet_colokmacau"]);
			win3_bet_colokmacau = parseFloat(record[i]["win3_bet_colokmacau"]);
			win4_bet_colokmacau = parseFloat(record[i]["win4_bet_colokmacau"]);
			limittotal_bet_colokmacau = parseInt(record[i]["limittotal_bet_colokmacau"]);
			min_bet_coloknaga = parseInt(record[i]["min_bet_coloknaga"]);
			max_bet_coloknaga = parseInt(record[i]["max_bet_coloknaga"]);
			disc_bet_coloknaga = parseFloat(record[i]["disc_bet_coloknaga"]);
			win_bet_coloknaga = parseFloat(record[i]["win_bet_coloknaga"]);
			win4_bet_coloknaga = parseFloat(record[i]["win4_bet_coloknaga"]);
			limittotal_bet_coloknaga = parseInt(record[i]["limittotal_bet_coloknaga"]);
			min_bet_colokjitu = parseInt(record[i]["min_bet_colokjitu"]);
			max_bet_colokjitu = parseInt(record[i]["max_bet_colokjitu"]);
			disc_bet_colokjitu = parseFloat(record[i]["disc_bet_colokjitu"]);
			winas_bet_colokjitu = parseFloat(record[i]["winas_bet_colokjitu"]);
			winkop_bet_colokjitu = parseFloat(record[i]["winkop_bet_colokjitu"]);
			winkepala_bet_colokjitu = parseFloat(record[i]["winkepala_bet_colokjitu"]);
			winekor_bet_colokjitu = parseFloat(record[i]["winekor_bet_colokjitu"]);
			limittotal_bet_colokjitu = parseInt(record[i]["limittotal_bet_colokjitu"]);
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
		count_line_colokbebas = 0;
		count_line_colokmacau = 0;
		count_line_coloknaga = 0;
		count_line_colokjitu = 0;
	}
	inittogel_432d("colok");
	function addKeranjang(
		nomor,game,
		bet,
		diskon_percen,diskon,
		bayar,win,kei,kei_percen,tipetoto) {
		let total_data = keranjang.length;
		let flag_data = false;
		for (var i = 0; i < total_data; i++) {
			switch (game) {
				case "COLOK_BEBAS":
					if (nomor == keranjang[i].nomor.toString()) {
						let maxtotal_bayarcolokbebas = 0;
						for (var j = 0; j < keranjang.length; j++) {
							if ("COLOK_BEBAS" == keranjang[j].permainan) {
								if (parseInt(nomor) == parseInt(keranjang[j].nomor)) {
									maxtotal_bayarcolokbebas = parseInt(maxtotal_bayarcolokbebas) + (parseInt(keranjang[j].bet) + parseInt(bet));
								}
							}
						}
						if (parseInt(limittotal_bet_colokbebas) <parseInt(maxtotal_bayarcolokbebas)) {
							temp_bulk_error +="Nomor ini : " + nomor +" sudah melebihi LIMIT TOTAL COLOK BEBAS<br />";
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
		let count_colokbebas = 0;
		let count_colokmacau = 0;
		let count_coloknaga = 0;
		let count_colokjitu = 0;
		for (let i = 0; i < keranjang.length; i++) {
			switch (keranjang[i].permainan.toString()) {
				case "COLOK_BEBAS":
					count_colokbebas = count_colokbebas + 1;
					break;
				case "COLOK_MACAU":
					count_colokmacau = count_colokmacau + 1;
					break;
				case "COLOK_NAGA":
					count_coloknaga = count_coloknaga + 1;
					break;
				case "COLOK_JITU":
					count_colokjitu = count_colokjitu + 1;
					break;
			}
		}
		count_line_colokbebas =
			count_colokbebas + db_formcolok_colokbebas_count_temp;
		count_line_colokmacau =
			count_colokmacau + db_formcolok_colokmacau_count_temp;
		count_line_coloknaga =
			count_coloknaga + db_formcolok_coloknaga_count_temp;
		count_line_colokjitu =
			count_colokjitu + db_formcolok_colokjitu_count_temp;
	}

	//COLOK BEBAS - INIT FORM
	let nomor_colokbebas = "";
	let nomor_colokbebas_input;
	let bet_colokbebas = "";

	//COLOK MACAU - INIT FORM
	let nomor_colokmacau_1 = "";
	let nomor_colokmacau_1_input;
	let nomor_colokmacau_2 = "";
	let nomor_colokmacau_2_input;
	let bet_colokmacau = "";

	//COLOK NAGA - INIT FORM
	let nomor_coloknaga_1 = "";
	let nomor_coloknaga_1_input;
	let nomor_coloknaga_2 = "";
	let nomor_coloknaga_2_input;
	let nomor_coloknaga_3 = "";
	let nomor_coloknaga_3_input;
	let bet_coloknaga = "";

	//COLOK JITU - INIT FORM
	let nomor_colokjitu = "";
	let nomor_colokjitu_input;
	let select_pilihancolokjitu = "";
	let select_pilihancolokjitu_input;
	let bet_colokjitu = "";

	//POLA COLOK - INIT FORM
	let nomor_polacolok = "";
	let nomor_polacolok_input;
	let bet_polacolokbebas = "";
	let bet_polacolokmacau = "";
	let bet_polacoloknaga = "";

	let flag_fulldiskon = "DISC"
	function form_clear(e) {
		switch (e) {
			case "colokbebas":
				nomor_colokbebas = "";
				nomor_colokbebas_input.focus();
				bet_colokbebas = 0;
				break;
			case "colokmacau":
				nomor_colokmacau_1 = "";
				nomor_colokmacau_2 = "";
				nomor_colokmacau_1_input.focus();
				bet_colokmacau = 0;
				break;
			case "coloknaga":
				nomor_coloknaga_1 = "";
				nomor_coloknaga_2 = "";
				nomor_coloknaga_3 = "";
				nomor_coloknaga_1_input.focus();
				bet_coloknaga = 0;
				break;
			case "colokjitu":
				nomor_colokjitu = "";
				select_pilihancolokjitu = "";
				nomor_colokjitu_input.focus();
				bet_colokjitu = 0;
				break;
			case "polacolok":
				nomor_polacolok = "";
				nomor_polacolok_input.focus();
				bet_polacolokbebas = "";
				bet_polacolokmacau = "";
				bet_polacoloknaga = "";
				break;
		}
	}
	function formcolokbebas_add() {
		let flag = true;
		let nomor = nomor_colokbebas;
		let bet = bet_colokbebas;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let nmgame = "COLOK_BEBAS";
		if (nomor == "") {
			nomor_colokbebas_input.focus();
			flag = false;
		}
		if (bet == "") {
			flag = false;
			alert("Amount tidak boleh kosong");
		}
		if (parseInt(bet) < parseInt(min_bet_colokbebas)) {
			flag = false;
			bet_colokbebas = min_bet_colokbebas;
			alert("Minimal Bet : " + min_bet_colokbebas);
		}
		if (parseInt(bet) > parseInt(max_bet_colokbebas)) {
			flag = false;
			bet_colokbebas = max_bet_colokbebas;
			alert("Maximal Bet : " + max_bet_colokbebas);
		}
		if (flag == true) {
			diskon = bet * disc_bet_colokbebas;
			diskonpercen = disc_bet_colokbebas;
			win = win_bet_colokbebas;
			bayar = parseInt(bet) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;

			addKeranjang(
				nomor,
				nmgame,
				bet_colokbebas,
				diskonpercen,
				diskon,
				bayar,
				win,
				0,
				0,flag_fulldiskon
			);
			form_clear("colokbebas");
			if (temp_bulk_error != "") {
				let myModal = new bootstrap.Modal(
					document.getElementById("modalError")
				);
				myModal.show();
			}
		}
	}
	function formcolokmacau_add() {
		let flag = true;
		let nomor = nomor_colokmacau_1;
		let nomor2 = nomor_colokmacau_2;
		let bet = bet_colokmacau;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let nmgame = "COLOK_MACAU";
		if (nomor == "") {
			nomor_colokmacau_1_input.focus();
			flag = false;
		}
		if (nomor2 == "") {
			flag = false;
		}
		if (nomor == nomor2) {
			alert("Nomor tidak boleh sama");
			flag = false;
			form_clear("colokmacau");
		}
		if (bet == "") {
			flag = false;
			alert("Amount tidak boleh kosong");
		}
		if (parseInt(bet) < parseInt(min_bet_colokmacau)) {
			bet_colokmacau = min_bet_colokmacau;
			flag = false;
			alert("Minimal Bet : " + min_bet_colokmacau);
		}
		if (parseInt(bet) > parseInt(max_bet_colokmacau)) {
			bet_colokmacau = max_bet_colokmacau;
			flag = false;
			alert("Maximal Bet : " + max_bet_colokmacau);
		}
		if (flag == true) {
			diskon = bet * disc_bet_colokmacau;
			diskonpercen = disc_bet_colokmacau;
			win = win_bet_colokmacau;
			bayar = parseInt(bet) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;

			addKeranjang(
				nomor + "" + nomor2,
				nmgame,
				bet_colokmacau,
				diskonpercen,
				diskon,
				bayar,
				win,
				0,
				0,flag_fulldiskon
			);
			form_clear("colokmacau");
		}
	}
	function formcoloknaga_add() {
		let flag = true;
		let nomor = nomor_coloknaga_1;
		let nomor2 = nomor_coloknaga_2;
		let nomor3 = nomor_coloknaga_3;
		let bet = bet_coloknaga;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let nmgame = "COLOK_NAGA";

		if (nomor == "") {
			nomor_coloknaga_1_input.focus();
			flag = false;
		}
		if (nomor2 == "") {
			nomor_coloknaga_2_input.focus();
			flag = false;
		}
		if (nomor3 == "") {
			nomor_coloknaga_3_input.focus();
			flag = false;
		}
		if (nomor == nomor2) {
			alert("Nomor tidak boleh sama");
			flag = false;
			form_clear("coloknaga");
		}
		if (nomor == nomor3) {
			alert("Nomor tidak boleh sama");
			flag = false;
			form_clear("coloknaga");
		}
		if (nomor2 == nomor3) {
			alert("Nomor tidak boleh sama");
			flag = false;
			form_clear("coloknaga");
		}
		if (bet == "") {
			flag = false;
			alert("Amount tidak boleh kosong");
		}
		if (parseInt(bet) < parseInt(min_bet_coloknaga)) {
			bet_coloknaga = min_bet_coloknaga;
			flag = false;
			alert("Minimal Bet : " + min_bet_coloknaga);
		}
		if (parseInt(bet) > parseInt(max_bet_coloknaga)) {
			bet_coloknaga = max_bet_coloknaga;
			flag = false;
			alert("Maximal Bet : " + max_bet_coloknaga);
		}
		if (flag == true) {
			diskon = bet * disc_bet_coloknaga;
			diskonpercen = disc_bet_coloknaga;
			win = win_bet_coloknaga;
			bayar = parseInt(bet) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;

			addKeranjang(
				nomor + "" + nomor2 + "" + nomor3,
				nmgame,
				bet_coloknaga,
				diskonpercen,
				diskon,
				bayar,
				win,
				0,
				0,flag_fulldiskon
			);
			form_clear("coloknaga");
		}
	}
	function formcolokjitu_add() {
		let flag = true;
		let nomor = nomor_colokjitu;
		let posisi = select_pilihancolokjitu;
		let bet = bet_colokjitu;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let nmgame = "COLOK_JITU";

		if (nomor == "") {
			nomor_colokjitu_input.focus();
			flag = false;
		}
		if (posisi == "") {
			select_pilihancolokjitu_input.focus();
			flag = false;
			alert("Posisi wajib diisi");
		}
		if (bet == "") {
			flag = false;
			alert("Amount tidak boleh kosong");
		}
		if (parseInt(bet) < parseInt(min_bet_colokjitu)) {
			bet_colokjitu = min_bet_colokjitu;
			flag = false;
			alert("Minimal Bet : " + min_bet_colokjitu);
		}
		if (parseInt(bet) > parseInt(max_bet_colokjitu)) {
			bet_colokjitu = max_bet_colokjitu;
			flag = false;
			alert("Maximal Bet : " + max_bet_colokjitu);
		}
		if (flag == true) {
			diskon = bet * disc_bet_colokjitu;
			diskonpercen = disc_bet_colokjitu;

			switch (posisi) {
				case "AS":
					win = winas_bet_colokjitu;
					break;
				case "KOP":
					win = winkop_bet_colokjitu;
					break;
				case "KEPALA":
					win = winkepala_bet_colokjitu;
					break;
				case "EKOR":
					win = winekor_bet_colokjitu;
					break;
			}

			bayar = parseInt(bet) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;

			addKeranjang(
				nomor + "_" + posisi,
				nmgame,
				bet_colokjitu,
				diskonpercen,
				diskon,
				bayar,
				win,
				0,
				0,flag_fulldiskon
			);
			form_clear("colokjitu");
		}
	}
	function formpolacolok_add() {
		let flag = true;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let found = false;
		let msg = "";
		if (nomor_polacolok == "") {
			nomor_polacolok.focus();
			flag = false;
		}
		if (nomor_polacolok.length<4 || nomor_polacolok.length>7) {
			nomor_polacolok_input.focus();
			flag = false;
			msg += "Minimal 4 Digit dan Maximal 7 Digit"
		}
		
		if(parseInt(bet_polacolokbebas) > 1){
			if (parseInt(bet_polacolokbebas) < parseInt(min_bet_colokbebas)) {
				flag = false;
				bet_polacolokbebas = min_bet_colokbebas;
				msg +=  "Minimal Bet Colok Bebas : " + min_bet_colokbebas;
			}
			if (parseInt(bet_polacolokbebas) > parseInt(max_bet_colokbebas)) {
				flag = false;
				bet_polacolokbebas = max_bet_colokbebas;
				msg +=  "Maximal Bet Colok Bebas : " + max_bet_colokbebas;
			}
			if(flag){
				for(let i=0;i<nomor_polacolok.length;i++){
					diskon = bet_polacolokbebas * disc_bet_colokbebas;
					diskonpercen = disc_bet_colokbebas;
					win = win_bet_colokbebas;
					bayar = parseInt(bet_polacolokbebas) - parseInt(Math.ceil(diskon));
					totalkeranjang = bayar + totalkeranjang;
					addKeranjang(
						nomor_polacolok[i],
						"COLOK_BEBAS",
						bet_polacolokbebas,
						diskonpercen,
						diskon,
						bayar,
						win,
						0,
						0,flag_fulldiskon
					);
				}
			}
		}
		if(parseInt(bet_polacolokmacau) > 1){
			let temp2d = []
			if (parseInt(bet_polacolokmacau) < parseInt(min_bet_colokmacau)) {
				flag = false;
				bet_polacolokmacau = min_bet_colokmacau;
				msg +=  "Minimal Bet Colok Macau : " + min_bet_colokmacau;
			}
			if (parseInt(bet_polacolokmacau) > parseInt(max_bet_colokmacau)) {
				flag = false;
				bet_polacolokmacau = max_bet_colokmacau;
				msg +=  "Maximal Bet Colok Macau : " + max_bet_colokmacau;
			}
			if(flag){
				let dat = ""
				for(let i=0;i<nomor_polacolok.length;i++){
					for(let j=0;j<nomor_polacolok.length;j++){
						dat = ""
						found = false
						if(nomor_polacolok[i] != nomor_polacolok[j]){
							dat =nomor_polacolok[i]+nomor_polacolok[j];
							found = true
						}
						if(found){
							if(dat != ""){
								temp2d.push(dat)
							}
						}
					}
				}
				for(let i=0;i<temp2d.length;i++){
					diskon = bet_polacolokmacau * disc_bet_colokmacau;
					diskonpercen = disc_bet_colokmacau;
					win = win_bet_colokmacau;
					bayar = parseInt(bet_polacolokmacau) - parseInt(Math.ceil(diskon));
					totalkeranjang = bayar + totalkeranjang;
					addKeranjang(
						temp2d[i],
						"COLOK_MACAU",
						bet_polacolokmacau,
						diskonpercen,
						diskon,
						bayar,
						win,
						0,
						0,flag_fulldiskon
					);
				}
			}
		}
		if(parseInt(bet_polacoloknaga) > 1){
			let temp3d = []
			if (parseInt(bet_polacoloknaga) < parseInt(min_bet_coloknaga)) {
				flag = false;
				bet_polacoloknaga = min_bet_coloknaga;
				msg +=  "Minimal Bet Colok Naga : " + min_bet_coloknaga;
			}
			if (parseInt(bet_polacoloknaga) > parseInt(max_bet_coloknaga)) {
				flag = false;
				bet_polacoloknaga = max_bet_coloknaga;
				msg +=  "Maximal Bet Colok Naga : " + max_bet_coloknaga;
			}
			if(flag){
				let dat = ""
				let flagcompare = false
				for(let i=0;i<nomor_polacolok.length;i++){
					for(let j=0;j<nomor_polacolok.length;j++){
						for(let x=0;x<nomor_polacolok.length;x++){
							dat = ""
							found = false
							flagcompare = true
							
							if(nomor_polacolok[i] == nomor_polacolok[j]){
								flagcompare = false
							}
							if(nomor_polacolok[i] == nomor_polacolok[x]){
								flagcompare = false
							}
							if(nomor_polacolok[j] == nomor_polacolok[x]){
								flagcompare = false
							}
							if(flagcompare){
								dat =nomor_polacolok[i]+nomor_polacolok[j]+nomor_polacolok[x];
								found = true
							}
							if(found){
								if(dat != ""){
									temp3d.push(dat)
								}
							}

							
						}
					}
				}
				for(let i=0;i<temp3d.length;i++){
					diskon = bet_polacoloknaga * disc_bet_coloknaga;
					diskonpercen = disc_bet_coloknaga;
					win = win_bet_coloknaga;
					bayar = parseInt(bet_polacoloknaga) - parseInt(Math.ceil(diskon));
					totalkeranjang = bayar + totalkeranjang;
					addKeranjang(
						temp3d[i],
						"COLOK_NAGA",
						bet_polacoloknaga,
						diskonpercen,
						diskon,
						bayar,
						win,
						0,
						0,flag_fulldiskon
					);
				}
			}
		}
		
		if(msg != ""){
			alert(msg)
		}
		form_clear("polacolok")
	}
	const handleTambah = (e) => {
		switch (e) {
			case "colokbebas":
				if (nomor_colokbebas == "" && parseInt(bet_colokbebas) < min_bet_colokbebas) {
					nomor_colokbebas_input.focus();
				} else {
					formcolokbebas_add();
				}
				break;
			case "colokmacau":
				if (nomor_colokmacau_1 == "" && nomor_colokmacau_2 == "" && parseInt(bet_colokmacau) < min_bet_colokmacau) {
					nomor_colokmacau_1_input.focus();
				} else {
					formcolokmacau_add();
				}
				break;
			case "coloknaga":
				if (nomor_coloknaga_1 == "" && nomor_coloknaga_2 == "" && nomor_coloknaga_3 == "" && parseInt(bet_coloknaga) < min_bet_coloknaga) {
					nomor_coloknaga_1_input.focus();
				} else {
					formcoloknaga_add();
				}
				break;
			case "colokjitu":
				if (nomor_colokjitu == "" && parseInt(bet_colokjitu) < min_bet_colokjitu) {
					nomor_colokjitu_input.focus();
				} else {
					formcolokjitu_add();
				}
				break;
			case "polacolok":
				if (nomor_polacolok == "") {
					nomor_polacolok_input.focus();
				} else {
					formpolacolok_add();
				}
				break;
		}
	};
	const handleKeyboard_format = (e) => {
		let numbera;
		for (let i = 0; i < nomor_colokbebas.length; i++) {
			numbera = parseInt(nomor_colokbebas[i]);
			if (isNaN(numbera)) {
				nomor_colokbebas = "";
			}
		}
		for (let i = 0; i < nomor_colokmacau_1.length; i++) {
			numbera = parseInt(nomor_colokmacau_1[i]);
			if (isNaN(numbera)) {
				nomor_colokmacau_1 = "";
			}
		}
		for (let i = 0; i < nomor_colokmacau_2.length; i++) {
			numbera = parseInt(nomor_colokmacau_2[i]);
			if (isNaN(numbera)) {
				nomor_colokmacau_2 = "";
			}
		}
		for (let i = 0; i < nomor_coloknaga_1.length; i++) {
			numbera = parseInt(nomor_coloknaga_1[i]);
			if (isNaN(numbera)) {
				nomor_coloknaga_1 = "";
			}
		}
		for (let i = 0; i < nomor_coloknaga_2.length; i++) {
			numbera = parseInt(nomor_coloknaga_2[i]);
			if (isNaN(numbera)) {
				nomor_coloknaga_2 = "";
			}
		}
		for (let i = 0; i < nomor_coloknaga_3.length; i++) {
			numbera = parseInt(nomor_coloknaga_3[i]);
			if (isNaN(numbera)) {
				nomor_coloknaga_3 = "";
			}
		}
		for (let i = 0; i < nomor_colokjitu.length; i++) {
			numbera = parseInt(nomor_colokjitu[i]);
			if (isNaN(numbera)) {
				nomor_colokjitu = "";
			}
		}
	};
	const handleKeyboard_number = (e) => {
		let numbera;
		for (let i = 0; i < bet_colokbebas.length; i++) {
			numbera = parseInt(bet_colokbebas[i]);
			if (isNaN(numbera)) {
				bet_colokbebas = "";
			}
		}
		for (let i = 0; i < bet_colokmacau.length; i++) {
			numbera = parseInt(bet_colokmacau[i]);
			if (isNaN(numbera)) {
				bet_colokmacau = "";
			}
		}
		for (let i = 0; i < bet_coloknaga.length; i++) {
			numbera = parseInt(bet_coloknaga[i]);
			if (isNaN(numbera)) {
				bet_coloknaga = "";
			}
		}
		for (let i = 0; i < bet_colokjitu.length; i++) {
			numbera = parseInt(bet_colokjitu[i]);
			if (isNaN(numbera)) {
				bet_colokjitu = "";
			}
		}
		for (let i = 0; i < nomor_polacolok.length; i++) {
			numbera = parseInt(nomor_polacolok[i]);
			if (isNaN(numbera)) {
				nomor_polacolok = "";
			}
		}
		for (let i = 0; i < bet_polacolokbebas.length; i++) {
			numbera = parseInt(bet_polacolokbebas[i]);
			if (isNaN(numbera)) {
				bet_polacolokbebas = "";
			}
		}
		for (let i = 0; i < bet_polacolokmacau.length; i++) {
			numbera = parseInt(bet_polacolokmacau[i]);
			if (isNaN(numbera)) {
				bet_polacolokmacau = "";
			}
		}
		for (let i = 0; i < bet_polacoloknaga.length; i++) {
			numbera = parseInt(bet_polacoloknaga[i]);
			if (isNaN(numbera)) {
				bet_polacoloknaga = "";
			}
		}
	};
	const handleKeyboard_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			formcolokbebas_add();
		}
	};
	const handleKeyboardcolokmacau_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			formcolokmacau_add();
		}
	};
	const handleKeyboardcoloknaga_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			formcoloknaga_add();
		}
	};
	const handleKeyboardcolokjitu_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			formcolokjitu_add();
		}
	};
	const handleKeyboardpolacolok_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			formpolacolok_add();
		}
	};
</script>

<Loader cssstyle={css_loader} />
{#if client_device == "WEBSITE"}
	<Card color="dark" style="border:1px solid #262424;">
		<CardHeader
			style="background:#323030;border-bottom:1px solid #333;border-top: 0 solid #333;">
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
			<ul class="nav nav-pills">
				<li class="nav-item">
				  <button
					class="nav-link active"
					id="pills-cbebas-tab"
					data-bs-toggle="pill"
					data-bs-target="#pills-cbebas"
					type="button"
					role="tab"
					aria-controls="pills-cbebas"
					aria-selected="true">BEBAS</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-cmacau-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-cmacau"
					  type="button"
					  role="tab"
					  aria-controls="pills-cmacau"
					  aria-selected="true">MACAU</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-cnaga-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-cnaga"
					  type="button"
					  role="tab"
					  aria-controls="pills-cnaga"
					  aria-selected="true">NAGA</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-cjitu-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-cjitu"
					  type="button"
					  role="tab"
					  aria-controls="pills-cjitu"
					  aria-selected="true">JITU</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-polacolok-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-polacolok"
					  type="button"
					  role="tab"
					  aria-controls="pills-polacolok"
					  aria-selected="true">POLA COLOK</button>
				</li>
			</ul>
			<div class="tab-content" id="nav-tabContent">
				<div class="tab-pane fade show active"
					id="pills-cbebas"
					role="tabpanel"
					aria-labelledby="pills-cbebas-tab">
					<div style="margin:5px;">
						<table class="table" style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (0-9)</span>
									<input
										autofocus
										bind:this={nomor_colokbebas_input}
										bind:value={nomor_colokbebas}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 1 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="1"
										maxlength="1"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">
										Bet (min : {new Intl.NumberFormat().format(
											min_bet_colokbebas
										)} dan max : {new Intl.NumberFormat().format(
											max_bet_colokbebas
										)})
									</span>
									<input
										bind:value={bet_colokbebas}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;">
										{new Intl.NumberFormat().format(
											bet_colokbebas
										)}
									</span>
								</td>
								<td
									width="20%"
									NOWRAP
									style="vertical-align: center;">
									<Button
										id="btn2"
										on:click={() => {
											handleTambah("colokbebas");
										}}>TAMBAH</Button>
								</td>
							</tr>
						</table>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-cmacau"
					role="tabpanel"
					aria-labelledby="pills-cmacau-tab">
					<table class="table" style="background:none;width:100%;">
						<tr>
							<td
								width="25%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;">
								<span style="color:#8a8a8a;">Nomor (0-9)</span>
								<input
									bind:this={nomor_colokmacau_1_input}
									bind:value={nomor_colokmacau_1}
									on:keyup={handleKeyboard_format}
									on:keypress={handleKeyboard_checkenter}
									type="text"
									class="form-control form-control-sm"
									placeholder="Input 1 Digit"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
									minlength="1"
									maxlength="1"
									tab_index="-1"
									autocomplete="off"/>
								<span
									class="help-block"
									style="text-align:right;font-size:12px;"/>
							</td>
							<td
								width="25%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;">
								<span style="color:#8a8a8a;">Nomor (0-9)</span>
								<input
									bind:this={nomor_colokmacau_2_input}
									bind:value={nomor_colokmacau_2}
									on:keyup={handleKeyboard_format}
									on:keypress={handleKeyboard_checkenter}
									type="text"
									class="form-control form-control-sm"
									placeholder="Input 1 Digit"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
									minlength="1"
									maxlength="1"
									tab_index="-1"
									autocomplete="off"/>
								<span
									class="help-block"
									style="text-align:right;font-size:12px;"/>
							</td>
							<td
								width="*"
								NOWRAP
								style="padding-right:10px;vertical-align: center;text-align:right;">
								<span style="color:#8a8a8a;"
									>Bet (min : {new Intl.NumberFormat().format(
										min_bet_colokmacau
									)} dan max : {new Intl.NumberFormat().format(
										max_bet_colokmacau
									)})
								</span>
								<input
									bind:value={bet_colokmacau}
									on:keyup={handleKeyboard_number}
									on:keypress={handleKeyboardcolokmacau_checkenter}
									type="text"
									class="form-control"
									placeholder="Bet"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
									minlength="3"
									maxlength="7"
									tab_index="0"/>
								<span
									style="text-align:right;font-size:12px;color:#8a8a8a;"
									>{new Intl.NumberFormat().format(
										bet_colokmacau
									)}
								</span>
							</td>
							<td
								width="20%"
								NOWRAP
								style="vertical-align: center;">
								<Button
									id="btn2"
									on:click={() => {
										handleTambah("colokmacau");
									}}>TAMBAH</Button>
							</td>
						</tr>
					</table>
				</div>
				<div class="tab-pane fade "
					id="pills-cnaga"
					role="tabpanel"
					aria-labelledby="pills-cnaga-tab">
					<table class="table" style="background:none;width:100%;">
						<tr>
							<td
								width="25%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;">
								<span style="color:#8a8a8a;">Nomor (0-9)</span>
								<input
									bind:this={nomor_coloknaga_1_input}
									bind:value={nomor_coloknaga_1}
									on:keyup={handleKeyboard_format}
									on:keypress={handleKeyboard_checkenter}
									type="text"
									class="form-control form-control-sm"
									placeholder="Input 1 Digit"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
									minlength="1"
									maxlength="1"
									tab_index="-1"
									autocomplete="off"/>
								<span
									class="help-block"
									style="text-align:right;font-size:12px;"/>
							</td>
							<td
								width="25%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;">
								<span style="color:#8a8a8a;">Nomor (0-9)</span>
								<input
									bind:this={nomor_coloknaga_2_input}
									bind:value={nomor_coloknaga_2}
									on:keyup={handleKeyboard_format}
									on:keypress={handleKeyboard_checkenter}
									type="text"
									class="form-control form-control-sm"
									placeholder="Input 1 Digit"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
									minlength="1"
									maxlength="1"
									tab_index="-1"
									autocomplete="off"/>
								<span
									class="help-block"
									style="text-align:right;font-size:12px;"/>
							</td>
							<td
								width="25%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;">
								<span style="color:#8a8a8a;">Nomor (0-9)</span>
								<input
									bind:this={nomor_coloknaga_3_input}
									bind:value={nomor_coloknaga_3}
									on:keyup={handleKeyboard_format}
									on:keypress={handleKeyboard_checkenter}
									type="text"
									class="form-control form-control-sm"
									placeholder="Input 1 Digit"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
									minlength="1"
									maxlength="1"
									tab_index="-1"
									autocomplete="off"/>
								<span
									class="help-block"
									style="text-align:right;font-size:12px;"/>
							</td>
							<td
								width="*"
								NOWRAP
								style="padding-right:10px;vertical-align: center;text-align:right;">
								<span style="color:#8a8a8a;">
									Bet (min : {new Intl.NumberFormat().format(
										min_bet_coloknaga
									)} dan max : {new Intl.NumberFormat().format(
										max_bet_coloknaga
									)})
								</span>
								<input
									bind:value={bet_coloknaga}
									on:keyup={handleKeyboard_number}
									on:keypress={handleKeyboardcoloknaga_checkenter}
									type="text"
									class="form-control"
									placeholder="Bet"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
									minlength="3"
									maxlength="7"
									tab_index="0"/>
								<span
									style="text-align:right;font-size:12px;color:#8a8a8a;"
									>{new Intl.NumberFormat().format(
										bet_coloknaga
									)}
								</span>
							</td>
							<td
								width="20%"
								NOWRAP
								style="vertical-align: center;">
								<Button
									id="btn2"
									on:click={() => {
										handleTambah("coloknaga");
									}}>TAMBAH</Button>
							</td>
						</tr>
					</table>
				</div>
				<div class="tab-pane fade "
					id="pills-cjitu"
					role="tabpanel"
					aria-labelledby="pills-cjitu-tab">
					<table class="table" style="background:none;width:100%;">
						<tr>
							<td
								width="25%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;">
								<span style="color:#8a8a8a;">Nomor (0-9)</span>
								<input
									bind:this={nomor_colokjitu_input}
									bind:value={nomor_colokjitu}
									on:keyup={handleKeyboard_format}
									on:keypress={handleKeyboard_checkenter}
									type="text"
									class="form-control form-control-sm"
									placeholder="Input 1 Digit"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
									minlength="1"
									maxlength="1"
									tab_index="-1"
									autocomplete="off"/>
								<span
									class="help-block"
									style="text-align:right;font-size:12px;"/>
							</td>
							<td
								width="15%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;">
								<div style="margin-top:-20px;">
									<span style="color:#8a8a8a;">Posisi</span>
									<select
										bind:value={select_pilihancolokjitu}
										bind:this={select_pilihancolokjitu_input}
										style="border:none;background:#303030;color:white;"
										class="form-control">
										<option value="">--Pilih--</option>
										<option value="AS">AS</option>
										<option value="KECIL">KOP</option>
										<option value="KEPALA">KEPALA</option>
										<option value="EKOR">EKOR</option>
									</select>
								</div>
							</td>
							<td
								width="*"
								NOWRAP
								style="padding-right:10px;vertical-align: center;text-align:right;">
								<span style="color:#8a8a8a;"
									>Bet (min : {new Intl.NumberFormat().format(
										min_bet_colokjitu
									)} dan max : {new Intl.NumberFormat().format(
										max_bet_colokjitu
									)})
								</span>
								<input
									bind:value={bet_colokjitu}
									on:keyup={handleKeyboard_number}
									on:keypress={handleKeyboardcolokjitu_checkenter}
									type="text"
									class="form-control"
									placeholder="Bet"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
									minlength="3"
									maxlength="7"
									tab_index="0"/>
								<span
									style="text-align:right;font-size:12px;color:#8a8a8a;"
									>{new Intl.NumberFormat().format(
										bet_colokjitu
									)}
								</span>
							</td>
							<td
								width="20%"
								NOWRAP
								style="vertical-align: center;">
								<Button
									id="btn2"
									on:click={() => {
										handleTambah("colokjitu");
									}}>TAMBAH</Button>
							</td>
						</tr>
					</table>
				</div>
				<div class="tab-pane fade "
					id="pills-polacolok"
					role="tabpanel"
					aria-labelledby="pills-polacolok-tab">
					<table class="table" style="background:none;width:100%;">
						<tr>
							<td
								width="25%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;">
								<span style="color:#8a8a8a;">Nomor (4 Digit / 7 Digit)</span>
								<input
									bind:this={nomor_polacolok_input}
									bind:value={nomor_polacolok}
									on:keyup={handleKeyboard_number}
									on:keypress={handleKeyboard_checkenter}
									type="text"
									class="form-control form-control-sm"
									placeholder="Input 4 / 7 Digit"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
									minlength="4"
									maxlength="7"
									tab_index="-1"
									autocomplete="off"/>
								<span
									class="help-block"
									style="text-align:right;font-size:12px;"/>
							</td>
							<td
								width="20%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;text-align:right;">
								<span style="color:#8a8a8a;">Bet Colok Bebas</span>
								<input
									bind:value={bet_polacolokbebas}
									on:keyup={handleKeyboard_number}
									on:keypress={handleKeyboardpolacolok_checkenter}
									type="text"
									class="form-control"
									placeholder="Bet"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
									minlength="3"
									maxlength="7"
									tab_index="0"/>
								<span
									style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
										bet_polacolokbebas
									)}
								</span>
							</td>
							<td
								width="20%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;text-align:right;">
								<span style="color:#8a8a8a;">Bet Colok Macau</span>
								<input
									bind:value={bet_polacolokmacau}
									on:keyup={handleKeyboard_number}
									on:keypress={handleKeyboardpolacolok_checkenter}
									type="text"
									class="form-control"
									placeholder="Bet"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
									minlength="3"
									maxlength="7"
									tab_index="0"/>
								<span
									style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
										bet_polacolokmacau
									)}
								</span>
							</td>
							<td
								width="20%"
								NOWRAP
								style="padding-right:10px;vertical-align: center;text-align:right;">
								<span style="color:#8a8a8a;">Bet Colok Naga</span>
								<input
									bind:value={bet_polacoloknaga}
									on:keyup={handleKeyboard_number}
									on:keypress={handleKeyboardpolacolok_checkenter}
									type="text"
									class="form-control"
									placeholder="Bet"
									style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
									minlength="3"
									maxlength="7"
									tab_index="0"/>
								<span
									style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
										bet_polacoloknaga
									)}
								</span>
							</td>
							<td
								width="*"
								NOWRAP
								style="vertical-align: center;">
								<Button
									id="btn2"
									on:click={() => {
										handleTambah("polacolok");
									}}>TAMBAH</Button>
							</td>
						</tr>
					</table>
				</div>
			</div>
		</CardBody>
	</Card>
{:else}
	<Card color="dark" style="border:1px solid #262424;margin:0px;padding:0px;">
		<CardHeader
			style="background:#323030;border-bottom:1px solid #333;border-top: 0 solid #333;">
			<div class="float-end">
				<div
					style="color:white;text-align:right;font-size:12px;font-weight:bold;">
					{pasaran_name}
				</div>
			</div>
			<h1 style="padding:0px;margin:0px;color:white;font-size:12px;">
				{permainan_title}<br />
				PERIODE : {pasaran_periode + " - " + pasaran_code}
			</h1>
		</CardHeader>
		<CardBody style="background:#121212;padding:0px;margin:0px;">
			<ul class="nav nav-pills">
				<li class="nav-item">
				  <button
					class="nav-link active"
					id="pills-cbebas-tab"
					data-bs-toggle="pill"
					data-bs-target="#pills-cbebas"
					type="button"
					role="tab"
					aria-controls="pills-cbebas"
					aria-selected="true">BEBAS</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-cmacau-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-cmacau"
					  type="button"
					  role="tab"
					  aria-controls="pills-cmacau"
					  aria-selected="true">MACAU</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-cnaga-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-cnaga"
					  type="button"
					  role="tab"
					  aria-controls="pills-cnaga"
					  aria-selected="true">NAGA</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-cjitu-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-cjitu"
					  type="button"
					  role="tab"
					  aria-controls="pills-cjitu"
					  aria-selected="true">JITU</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-polacolok-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-polacolok"
					  type="button"
					  role="tab"
					  aria-controls="pills-polacolok"
					  aria-selected="true">POLA COLOK</button>
				</li>
			</ul>
			<div class="tab-content" id="nav-tabContent">
				<div class="tab-pane fade show active"
					id="pills-cbebas"
					role="tabpanel"
					aria-labelledby="pills-cbebas-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (0-9)</span>
									<input
										bind:this={nomor_colokbebas_input}
										bind:value={nomor_colokbebas}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 1 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="1"
										maxlength="1"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;"
										>Bet (min : {new Intl.NumberFormat().format(
											min_bet_colokbebas
										)} dan max : {new Intl.NumberFormat().format(
											max_bet_colokbebas
										)})</span>
									<input
										bind:value={bet_colokbebas}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_colokbebas
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("colokbebas");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-cmacau"
					role="tabpanel"
					aria-labelledby="pills-cmacau-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (0-9)</span>
									<input
										bind:this={nomor_colokmacau_1_input}
										bind:value={nomor_colokmacau_1}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 1 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="1"
										maxlength="1"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (0-9)</span>
									<input
										bind:this={nomor_colokmacau_2_input}
										bind:value={nomor_colokmacau_2}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 1 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="1"
										maxlength="1"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
							</tr>
							<tr>
								<td
									colspan="2"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;"
										>Bet (min : {new Intl.NumberFormat().format(
											min_bet_colokmacau
										)} dan max : {new Intl.NumberFormat().format(
											max_bet_colokmacau
										)})</span>
									<input
										bind:value={bet_colokmacau}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardcolokmacau_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_colokmacau
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("colokmacau");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-cnaga"
					role="tabpanel"
					aria-labelledby="pills-cnaga-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (0-9)</span>
									<input
										bind:this={nomor_coloknaga_1_input}
										bind:value={nomor_coloknaga_1}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 1 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="1"
										maxlength="1"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (0-9)</span>
									<input
										bind:this={nomor_coloknaga_2_input}
										bind:value={nomor_coloknaga_2}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 1 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="1"
										maxlength="1"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (0-9)</span>
									<input
										bind:this={nomor_coloknaga_3_input}
										bind:value={nomor_coloknaga_3}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 1 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="1"
										maxlength="1"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
							</tr>
							<tr>
								<td
									colspan="3"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;"
										>Bet (min : {new Intl.NumberFormat().format(
											min_bet_coloknaga
										)} dan max : {new Intl.NumberFormat().format(
											max_bet_coloknaga
										)})</span>
									<input
										bind:value={bet_coloknaga}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardcoloknaga_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_coloknaga
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("coloknaga");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-cjitu"
					role="tabpanel"
					aria-labelledby="pills-cjitu-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (0-9)</span>
									<input
										bind:this={nomor_colokjitu_input}
										bind:value={nomor_colokjitu}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 1 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="1"
										maxlength="1"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<div style="margin-top:-20px;">
										<span style="color:#8a8a8a;">Posisi</span>
										<select
											bind:value={select_pilihancolokjitu}
											bind:this={select_pilihancolokjitu_input}
											style="border:none;background:#303030;color:white;"
											class="form-control">
											<option value="">--Pilih--</option>
											<option value="AS">AS</option>
											<option value="KECIL">KOP</option>
											<option value="KEPALA">KEPALA</option>
											<option value="EKOR">EKOR</option>
										</select>
									</div>
								</td>
							</tr>
							<tr>
								<td
									colspan="2"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;"
										>Bet (min : {new Intl.NumberFormat().format(
											min_bet_colokjitu
										)} dan max : {new Intl.NumberFormat().format(
											max_bet_colokjitu
										)})</span>
									<input
										bind:value={bet_colokjitu}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardcolokjitu_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_colokjitu
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("colokjitu");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-polacolok"
					role="tabpanel"
					aria-labelledby="pills-polacolok-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td 
									NOWRAP
									style="padding-right:10px;vertical-align: center;"
									colspan="3">
									<span style="color:#8a8a8a;">Nomor (4 Digit / 7 Digit)</span>
									<input
										bind:this={nomor_polacolok_input}
										bind:value={nomor_polacolok}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 4 / 7 Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="7"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
							</tr>
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet Colok Bebas</span>
									<input
										bind:value={bet_polacolokbebas}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardpolacolok_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span style="text-align:right;font-size:12px;color:#8a8a8a;">
										{new Intl.NumberFormat().format(
											bet_polacolokbebas
										)}
									</span>
								</td>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet Colok Macau</span>
									<input
										bind:value={bet_polacolokmacau}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardpolacolok_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span style="text-align:right;font-size:12px;color:#8a8a8a;">
										{new Intl.NumberFormat().format(
											bet_polacolokmacau
										)}
									</span>
								</td>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet Colok Naga</span>
									<input
										bind:value={bet_polacoloknaga}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardpolacolok_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
											bet_polacoloknaga
										)}
									</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("polacolok");
							}}>TAMBAH</Button>
					</div>
				</div>
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
				alt=""/>
		</div>
		<h5 class="modal-title" id="exampleModalLabel">ERROR</h5>
	</slot:template>
	<slot:template slot="body">
		{@html temp_bulk_error}
	</slot:template>
</Modal>
<div class="clearfix" />
<br />
<Tablekeranjangcolok
	on:removekeranjang={removekeranjang}
	on:removekeranjangall={removekeranjangall}
	on:handleSave={handleSave}
	{client_device}
	{group_btn_beli}
	{count_line_colokbebas}
	{count_line_colokmacau}
	{count_line_coloknaga}
	{count_line_colokjitu}
	{keranjang}
	{totalkeranjang}
	{min_bet_colokbebas}
	{max_bet_colokbebas}
	{disc_bet_colokbebas}
	{win_bet_colokbebas}
	{min_bet_colokmacau}
	{max_bet_colokmacau}
	{disc_bet_colokmacau}
	{win_bet_colokmacau}
	{win3_bet_colokmacau}
	{win4_bet_colokmacau}
	{min_bet_coloknaga}
	{max_bet_coloknaga}
	{disc_bet_coloknaga}
	{win_bet_coloknaga}
	{win4_bet_coloknaga}
	{min_bet_colokjitu}
	{max_bet_colokjitu}
	{disc_bet_colokjitu}
	{winas_bet_colokjitu}
	{winkop_bet_colokjitu}
	{winkepala_bet_colokjitu}
	{winekor_bet_colokjitu}
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
