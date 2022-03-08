<script>
	import {
		Button,
		Card,
		CardBody,
		CardHeader,
	} from "sveltestrap";
	import Modal from "../components/Modal.svelte";
	import Modal2 from "../components/Modalpilihan.svelte";
	import Tablekeranjang from "../permainan/Tablekeranjang.svelte";
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
	export let permainan_title = "4D / 3D / 2D";

	let keranjang = [];
	let css_loader = "display:none;";
	let nomor_global = 0;
	let totalkeranjang = 0;
	let group_btn_beli = false;
	let record = "";
	let minimal_bet = 0;
	let max4d_bet = 0;
	let max3d_bet = 0;
	let max3dd_bet = 0;
	let max2d_bet = 0;
	let max2dd_bet = 0;
	let max2dt_bet = 0;
	let disc4d_bet = 0;
	let disc3d_bet = 0;
	let disc3dd_bet = 0;
	let disc2d_bet = 0;
	let disc2dd_bet = 0;
	let disc2dt_bet = 0;
	let win4d_bet = 0;
	let win3d_bet = 0;
	let win3dd_bet = 0;
	let win2d_bet = 0;
	let win2dd_bet = 0;
	let win2dt_bet = 0;
	let win4dnodiskon_bet = 0;
	let win3dnodiskon_bet = 0;
	let win3ddnodiskon_bet = 0;
	let win2dnodiskon_bet = 0;
	let win2ddnodiskon_bet = 0;
	let win2dtnodiskon_bet = 0;
	let win4dbb_kena_bet = 0;
	let win3dbb_kena_bet = 0;
	let win3ddbb_kena_bet = 0;
	let win2dbb_kena_bet = 0;
	let win2ddbb_kena_bet = 0;
	let win2dtbb_kena_bet = 0;
	let win4dbb_bet = 0;
	let win3dbb_bet = 0;
	let win3ddbb_bet = 0;
	let win2dbb_bet = 0;
	let win2ddbb_bet = 0;
	let win2dtbb_bet = 0;
	let limittotal4d_bet = 0;
	let limittotal3d_bet = 0;
	let limittotal3dd_bet = 0;
	let limittotal2d_bet = 0;
	let limittotal2dd_bet = 0;
	let limittotal2dt_bet = 0;
	let limitline_4d = 0;
	let limitline_3d = 0;
	let limitline_3dd = 0;
	let limitline_2d = 0;
	let limitline_2dd = 0;
	let limitline_2dt = 0;
	let bbfs = 0;

	let count_line_4d = 0;
	let count_line_3d = 0;
	let count_line_3dd = 0;
	let count_line_2d = 0;
	let count_line_2dd = 0;
	let count_line_2dt = 0;

	let db_form4d_4d_count_temp = 0;
	let db_form4d_3d_count_temp = 0;
	let db_form4d_3dd_count_temp = 0;
	let db_form4d_2d_count_temp = 0;
	let db_form4d_2dd_count_temp = 0;
	let db_form4d_2dt_count_temp = 0;

	let flag_fulldiskon = "DISC"
	let path_432 = ""
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
		minimal_bet = record[0]["min_bet"];
		for (var i = 0; i < record.length; i++) {
			minimal_bet = parseInt(record[i]["min_bet"]);
			max4d_bet = parseInt(record[i]["max4d_bet"]);
			max3d_bet = parseInt(record[i]["max3d_bet"]);
			max3dd_bet = parseInt(record[i]["max3dd_bet"]);
			max2d_bet = parseInt(record[i]["max2d_bet"]);
			max2dd_bet = parseInt(record[i]["max2dd_bet"]);
			max2dt_bet = parseInt(record[i]["max2dt_bet"]);
			disc4d_bet = parseFloat(record[i]["disc4d_bet"]);
			disc3d_bet = parseFloat(record[i]["disc3d_bet"]);
			disc3dd_bet = parseFloat(record[i]["disc3dd_bet"]);
			disc2d_bet = parseFloat(record[i]["disc2d_bet"]);
			disc2dd_bet = parseFloat(record[i]["disc2dd_bet"]);
			disc2dt_bet = parseFloat(record[i]["disc2dt_bet"]);
			win4d_bet = parseInt(record[i]["win4d_bet"]);
			win3d_bet = parseInt(record[i]["win3d_bet"]);
			win3dd_bet = parseInt(record[i]["win3dd_bet"]);
			win2d_bet = parseInt(record[i]["win2d_bet"]);
			win2dd_bet = parseInt(record[i]["win2dd_bet"]);
			win2dt_bet = parseInt(record[i]["win2dt_bet"]);
			win4dnodiskon_bet = parseInt(record[i]["win4dnodiskon_bet"]);
			win3dnodiskon_bet = parseInt(record[i]["win3dnodiskon_bet"]);
			win3ddnodiskon_bet = parseInt(record[i]["win3ddnodiskon_bet"]);
			win2dnodiskon_bet = parseInt(record[i]["win2dnodiskon_bet"]);
			win2ddnodiskon_bet = parseInt(record[i]["win2ddnodiskon_bet"]);
			win2dtnodiskon_bet = parseInt(record[i]["win2dtnodiskon_bet"]);
			win4dbb_kena_bet = parseInt(record[i]["win4dbb_kena_bet"]);
			win3dbb_kena_bet = parseInt(record[i]["win3dbb_kena_bet"]);
			win3ddbb_kena_bet = parseInt(record[i]["win3ddbb_kena_bet"]);
			win2dbb_kena_bet = parseInt(record[i]["win2dbb_kena_bet"]);
			win2ddbb_kena_bet = parseInt(record[i]["win2ddbb_bet"]);
			win2dtbb_kena_bet = parseInt(record[i]["win2dtbb_kena_bet"]);
			win4dbb_bet = parseInt(record[i]["win4dbb_bet"]);
			win3dbb_bet = parseInt(record[i]["win3dbb_bet"]);
			win3ddbb_bet = parseInt(record[i]["win3dd_bet"]);
			win2dbb_bet = parseInt(record[i]["win2dbb_bet"]);
			win2ddbb_bet = parseInt(record[i]["win2ddbb_bet"]);
			win2dtbb_bet = parseInt(record[i]["win2dtbb_bet"]);
			limittotal4d_bet = parseInt(record[i]["limittotal4d_bet"]);
			limittotal3d_bet = parseInt(record[i]["limittotal3d_bet"]);
			limittotal3dd_bet = parseInt(record[i]["limittotal3dd_bet"]);
			limittotal2d_bet = parseInt(record[i]["limittotal2d_bet"]);
			limittotal2dd_bet = parseInt(record[i]["limittotal2dd_bet"]);
			limittotal2dt_bet = parseInt(record[i]["limittotal2dt_bet"]);
			limitline_4d = parseInt(record[i]["limitline_4d"]);
			limitline_3d = parseInt(record[i]["limitline_3d"]);
			limitline_3dd = parseInt(record[i]["limitline_3dd"]);
			limitline_2d = parseInt(record[i]["limitline_2d"]);
			limitline_2dd = parseInt(record[i]["limitline_2dd"]);
			limitline_2dt = parseInt(record[i]["limitline_2dt"]);
			bbfs = parseInt(record[i]["bbfs"]);
		}
	}
	async function limittogel(e) {
		db_form4d_4d_count_temp = 0;
		db_form4d_3d_count_temp = 0;
		db_form4d_3dd_count_temp = 0;
		db_form4d_2d_count_temp = 0;
		db_form4d_2dd_count_temp = 0;
		db_form4d_2dt_count_temp = 0;
		const res = await fetch("/api/limittogel", {
			method: "POST",
			headers: {
				"Content-Type": "application/json",
			},
			body: JSON.stringify({
				pasaran_idtransaction: parseInt(idtrxkeluaran),
				company: client_company,
				username: client_username,
				pasaran_code: pasaran_code,
				pasaran_periode: pasaran_periode,
				permainan: e,
			}),
		});
		const json = await res.json();
		record = json.record;

		db_form4d_4d_count_temp = record.total_4d;
		db_form4d_3d_count_temp = record.total_3d;
		db_form4d_3dd_count_temp = record.total_3dd;
		db_form4d_2d_count_temp = record.total_2d;
		db_form4d_2dd_count_temp = record.total_2dd;
		db_form4d_2dt_count_temp = record.total_2dt;

		count_line_4d = count_line_4d + db_form4d_4d_count_temp;
		count_line_3d = count_line_3d + db_form4d_3d_count_temp;
		count_line_3dd = count_line_3dd + db_form4d_3dd_count_temp;
		count_line_2d = count_line_2d + db_form4d_2d_count_temp;
		count_line_2dd = count_line_2dd + db_form4d_2dd_count_temp;
		count_line_2dt = count_line_2dt + db_form4d_2dt_count_temp;
	}
	async function savetransaksi() {
		if (client_device == "WEBSITE") {
			css_loader = "position:absolute;z-index: 1000;left: 50%;top: 35%;display:inline;";
		} else {
			css_loader = "position:absolute;z-index: 1000;left: 40%;top: 50%;display:inline;";
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
		count_line_4d = 0;
		count_line_3d = 0;
		count_line_3dd = 0;
		count_line_2d = 0;
		count_line_2dd = 0;
		count_line_2dt = 0;
		temp_bulk_error = "";
		limittogel("4-3-2");
	}
	inittogel_432d("4-3-2");
	limittogel("4-3-2");
	function addKeranjang(
		nomor,
		game,
		bet,
		diskon_percen,
		diskon,
		bayar,
		win,
		kei,
		kei_percen,tipetoto) {
		let total_data = keranjang.length;
		let flag_data = false;
		for (var i = 0; i < total_data; i++) {
			switch (game) {
				case "4D":
					if (nomor == keranjang[i].nomor.toString()) {
						let maxtotal_bayar4d = 0;
						for (var j = 0; j < keranjang.length; j++) {
							if ("4D" == keranjang[j].permainan) {
								if (parseInt(nomor) ==parseInt(keranjang[j].nomor)) {
									maxtotal_bayar4d =parseInt(maxtotal_bayar4d) +(parseInt(keranjang[j].bet) +parseInt(bet));
								}
							}
						}
						if (parseInt(limittotal4d_bet) < parseInt(maxtotal_bayar4d)) {
							temp_bulk_error +="Nomor ini : " +nomor +" sudah melebihi LIMIT TOTAL 4D<br />";
							flag_data = true;
						}
					}
					break;
				case "3D":
					if (nomor == keranjang[i].nomor.toString()) {
						let maxtotal_bayar3d = 0;
						for (var j = 0; j < keranjang.length; j++) {
							if ("3D" == keranjang[j].permainan) {
								if (parseInt(nomor) ==parseInt(keranjang[j].nomor)) {
									maxtotal_bayar3d =parseInt(maxtotal_bayar3d) +(parseInt(keranjang[j].bet) +parseInt(bet));
								}
							}
						}

						if (parseInt(limittotal3d_bet) < parseInt(maxtotal_bayar3d)) {
							temp_bulk_error +="Nomor ini : " +nomor +" sudah melebihi LIMIT TOTAL 3D<br />";
							flag_data = true;
						}
					}
					break;
				case "3DD":
					if (nomor == keranjang[i].nomor.toString()) {
						let maxtotal_bayar3dd = 0;
						for (var j = 0; j < keranjang.length; j++) {
							if ("3DD" == keranjang[j].permainan) {
								if (parseInt(nomor) == parseInt(keranjang[j].nomor)) {
									maxtotal_bayar3dd = parseInt(maxtotal_bayar3dd) + (parseInt(keranjang[j].bet) + parseInt(bet));
								}
							}
						}

						if (parseInt(limittotal3dd_bet) < parseInt(maxtotal_bayar3dd)) {
							temp_bulk_error += "Nomor ini : " +nomor +" sudah melebihi LIMIT TOTAL 3DD<br />";
							flag_data = true;
						}
					}
					break;
				case "2D":
					if (nomor == keranjang[i].nomor.toString()) {
						let maxtotal_bayar2d = 0;
						for (var j = 0; j < keranjang.length; j++) {
							if ("2D" == keranjang[j].game) {
								if (parseInt(nomor) ==parseInt(keranjang[j].nomor)) {
									maxtotal_bayar2d =parseInt(maxtotal_bayar2d) +(parseInt(keranjang[j].bet) +parseInt(bet));
								}
							}
						}

						if (parseInt(limittotal2d_bet) <parseInt(maxtotal_bayar2d)) {
							temp_bulk_error +="Nomor ini : " +nomor +" sudah melebihi LIMIT TOTAL 2D<br />";
							flag_data = true;
						}
					}
					break;
				case "2DD":
					if (nomor == keranjang[i].nomor.toString()) {
						let maxtotal_bayar2dd = 0;
						for (var j = 0; j < keranjang.length; j++) {
							if ("2DD" == keranjang[j].game) {
								if (
									parseInt(nomor) ==
									parseInt(keranjang[j].nomor)
								) {
									maxtotal_bayar2dd =
										parseInt(maxtotal_bayar2dd) +
										(parseInt(keranjang[j].bet) +
											parseInt(bet));
								}
							}
						}
						if (parseInt(limittotal2dd_bet) < parseInt(maxtotal_bayar2dd)) {
							temp_bulk_error += "Nomor ini : " +nomor + " sudah melebihi LIMIT TOTAL 2DD<br />";
							flag_data = true;
						}
					}
					break;
				case "2DT":
					if (nomor == keranjang[i].nomor.toString()) {
						let maxtotal_bayar2dt = 0;
						for (var j = 0; j < keranjang.length; j++) {
							if ("2DT" == keranjang[j].game) {
								if (parseInt(nomor) == parseInt(keranjang[j].nomor)) {
									maxtotal_bayar2dt =parseInt(maxtotal_bayar2dt) + (parseInt(keranjang[j].bet) + parseInt(bet));
								}
							}
						}
						if (parseInt(limittotal2dt_bet) <parseInt(maxtotal_bayar2dt)) {
							temp_bulk_error += "Nomor ini : " + nomor +" sudah melebihi LIMIT TOTAL 2DT<br />";
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
				kei_percen,
				tipetoto,
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
		let count_4d = 0;
		let count_3d = 0;
		let count_3dd = 0;
		let count_2d = 0;
		let count_2dd = 0;
		let count_2dt = 0;
		for (let i = 0; i < keranjang.length; i++) {
			switch (keranjang[i].permainan.toString()) {
				case "4D":
					count_4d = count_4d + 1;
					break;
				case "3D":
					count_3d = count_3d + 1;
					break;
				case "3DD":
					count_3dd = count_3dd + 1;
					break;
				case "2D":
					count_2d = count_2d + 1;
					break;
				case "2DD":
					count_2dd = count_2dd + 1;
					break;
				case "2DT":
					count_2dt = count_2dt + 1;
					break;
			}
		}
		count_line_4d = count_4d + db_form4d_4d_count_temp;
		count_line_3d = count_3d + db_form4d_3d_count_temp;
		count_line_3dd = count_3dd + db_form4d_3dd_count_temp;
		count_line_2d = count_2d + db_form4d_2d_count_temp;
		count_line_2dd = count_2dd + db_form4d_2dd_count_temp;
		count_line_2dt = count_2dt + db_form4d_2dt_count_temp;
	}

	//432 - INIT FORM
	let nomor_432 = "";
	let nomor_432_input;
	let bet_432 = "";
	//SET - INIT FORM
	let nomorset = "";
	let nomorset_input;
	let betset_1 = "";
	let betset_2 = "";
	let betset_3 = "";
	let betset_4 = "";
	let betset_5 = "";
	let betset_6 = "";
	//BBFS - INIT FORM
	let nomorbbfs = "";
	let nomorbbfs_input;
	let bet_1 = "";
	let bet_2 = "";
	let bet_3 = "";
	let bet_4 = "";
	let bet_5 = "";
	let bet_6 = "";
	//WAP
	let nomorwap = "";
	let nomorwap_input;
	//pola tarung
	let nomoras = "";
	let nomoras_input;
	let nomorkop = "";
	let nomorkop_input;
	let nomorkepala = "";
	let nomorekor = "";
	let bet_tarung = "";
	let bet_tarung_input;
	//3DD - INIT FORM
	let nomor3dd = "";
	let nomor3dd_input;
	let bet_3dd = "";
	//2DD - INIT FORM
	let nomor2dd = "";
	let nomor2dd_input;
	let bet_2dd = "";
	//2DT - INIT FORM
	let nomor2dt = "";
	let nomor2dt_input;
	let bet_2dt = "";
	//QUICK 2D
	let quick_pilihan1;
	let quick_pilihan2;
	let quick_bet = "";
	let quick_pilihan1_input;
	let quick_pilihan2_input;
	let quick_bet_input;

	let generate2D = [];
	let generate2DD = [];
	let generate2DT = [];
	let generate3D = [];
	let generate3DD = [];
	let generate4D = [];
	let data_bbfs = [];
	let nol = 0;
	let satu = 0;
	let dua = 0;
	let tiga = 0;
	let empat = 0;
	let lima = 0;
	let enam = 0;
	let tujuh = 0;
	let delapan = 0;
	let sembilan = 0;
	let temp_bulk_error = "";
	function form_clear(e) {
		switch (e) {
			case "4-3-2":
				nomor_432 = "";
				nomor_432_input.focus();
				bet_432 = "";
				break;
			case "432SET":
				nomorset = "";
				nomorset_input.focus();
				betset_1 = "";
				betset_2 = "";
				betset_3 = "";
				betset_4 = "";
				betset_5 = "";
				betset_6 = "";
				break;
			case "bbfs":
				nomorbbfs = "";
				nomorbbfs_input.focus();
				bet_432 = "";
				bet_1 = "";
				bet_2 = "";
				bet_3 = "";
				bet_4 = "";
				bet_5 = "";
				bet_6 = "";
				break;
			case "wap":
				nomorwap = "";
				nomorwap_input.focus();
				break;
			case "polatarung":
				nomoras = "";
				nomoras_input.focus();
				nomorkop = "";
				nomorkepala = "";
				nomorekor = "";
				bet_tarung = "";
				break;
			case "3DD":
				nomor3dd = "";
				nomor3dd_input.focus();
				bet_3dd = "";
				break;
			case "2DD":
				nomor2dd = "";
				nomor2dd_input.focus();
				bet_2dd = "";
				break;
			case "2DT":
				nomor2dt = "";
				nomor2dt_input.focus();
				bet_2dt = "";
				break;
			case "quick2D":
				quick_pilihan1;
				quick_pilihan2;
				quick_bet = "";
				quick_pilihan1_input;
				quick_pilihan2_input;
				quick_bet_input.focus();
				break;
		}
	}
	function form4d_add() {
		let flag = true;
		let game = nomor_432.length;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let nmgame = "";
		let msg = "";
		if (nomor_432 == "") {
			nomor_432_input.focus();
			flag = false;
		}
		let tempbintang = 0;
		let tempnumber = 0;
		for (let i = 0; i <= 3; i++) {
			if (nomor_432[i] == "*") {
				tempbintang = tempbintang + 1;
			}
			let numbera = parseInt(nomor_432[i])
			if (!isNaN(numbera)) {
				tempnumber = tempnumber + 1;
			}
		}
		
		if (tempbintang > 2) {
			flag = false;
			form_clear("4-3-2");
			nomor_input.focus();
			msg += "Format Salah\nContoh:\n4D: 1234\n3D: 123\n3DD: 123*\n2D: 12 atau **10\n2DD: 10**\n2DT: *10*\n";
		}
		if (nomor_432[3] == "*" && parseInt(tempnumber) == 3) {
			nomor_432 = String(nomor_432[0]) + String(nomor_432[1])+ String(nomor_432[2]);
			game = "3DD";
		}
		if (nomor_432[0] == "*" && parseInt(tempnumber) == 3) {
			nomor_432 = String(nomor_432[1]) + String(nomor_432[2])+ String(nomor_432[3]);
			game = "3";
		}
		if (nomor_432[0] == "*" && nomor_432[1] == "*" && parseInt(tempnumber) == 2) {
			nomor_432 = String(nomor_432[2]) + String(nomor_432[3]);
			game = "2";
		}
		if (nomor_432[2] == "*" && nomor_432[3] == "*" && parseInt(tempnumber) == 2) {
			nomor_432 = String(nomor_432[0]) + String(nomor_432[1]);
			game = "2DD";
		}
		if (nomor_432[0] == "*" && nomor_432[3] == "*" && parseInt(tempnumber) == 2) {
			nomor_432 = String(nomor_432[1]) + String(nomor_432[2]);
			game = "2DT";
		}
		if (nomor_432.length < 2) {
			flag = false;
			nomor_432_input.focus();
			nomor_432 = "";
			msg += "Minimal Nomor 2 Digit"+"\n";
		}
		if (bet_432 == "") {
			flag = false;
			msg += "Bet tidak boleh kosong"+"\n";
		}
		if (parseInt(bet_432) < parseInt(minimal_bet)) {
			bet_432 = minimal_bet;
			flag = false;
			msg += "Minimal Bet : " + new Intl.NumberFormat().format(minimal_bet)+"\n";
		}
		if (game.toString() == "4") {
			if (parseInt(bet_432) > parseInt(max4d_bet)) {
				bet_432 = minimal_bet;
				flag = false;
				msg += "Maximal Bet 4D : " +new Intl.NumberFormat().format(max4d_bet)+"\n";
			}
			if (checkLimitLine("4D") == false) {
				flag = false;
				msg += "Maximal Line 4D : " + limitline_4d+"\n";
				form_clear("4-3-2");
			}
		}
		if (game.toString() == "3") {
			if (parseInt(bet_432) > parseInt(max3d_bet)) {
				bet_432 = minimal_bet;
				flag = false;
				msg += "Maximal Bet 3D : " +new Intl.NumberFormat().format(max3d_bet)+"\n";
			}
			if (checkLimitLine("3D") == false) {
				flag = false;
				msg += "Maximal Line 3D : " + limitline_3d+"\n";
				form_clear("4-3-2");
			}
			if(parseInt(tempnumber) != 3){
				flag = false;
				msg += "Format Nomor 3D Salah \n";
				form_clear("4-3-2");
			}
		}
		if (game.toString() == "3DD") {
			if (parseInt(bet_432) > parseInt(max3dd_bet)) {
				bet_432 = minimal_bet;
				flag = false;
				msg += "Maximal Bet 3DD : " +new Intl.NumberFormat().format(max3dd_bet)+"\n";
			}
			if (checkLimitLine("3DD") == false) {
				flag = false;
				msg += "Maximal Line 3DD : " + limitline_3dd+"\n";
				form_clear("4-3-2");
			}
			if(parseInt(tempnumber) != 3){
				flag = false;
				msg += "Format Nomor 3D Salah \n";
				form_clear("4-3-2");
			}
		}
		if (game.toString() == "2") {
			if (parseInt(bet_432) > parseInt(max2d_bet)) {
				bet_432 = minimal_bet;
				flag = false;
				msg += "Maximal Bet 2D : " + new Intl.NumberFormat().format(max2d_bet)+"\n";
			}
			if (checkLimitLine("2D") == false) {
				flag = false;
				msg +="Maximal Line 2D : " + limitline_2d+"\n";
				form_clear("4-3-2");
			}
			if(parseInt(tempnumber) != 2){
				flag = false;
				msg += "Format Nomor 2D Salah \n";
				form_clear("4-3-2");
			}
		}
		if (game.toString() == "2DD") {
			if (parseInt(bet_432) > parseInt(max2dd_bet)) {
				bet_432 = minimal_bet;
				flag = false;
				msg += "Maximal Bet 2D : " +new Intl.NumberFormat().format(max2dd_bet)+"\n";
			}
			if (checkLimitLine("2DD") == false) {
				flag = false;
				msg += "Maximal Line 2DD : " + limitline_2dd;
				form_clear("4-3-2");
			}
			if(parseInt(tempnumber) != 2){
				flag = false;
				msg += "Format Nomor 2D Salah \n";
				form_clear("4-3-2");
			}
		}
		if (game.toString() == "2DT") {
			if (parseInt(bet_432) > parseInt(max2dt_bet)) {
				bet = minimal_bet;
				flag = false;
				msg += "Maximal Bet 2DT : " +new Intl.NumberFormat().format(max2dt_bet)+"\n";
			}
			if (checkLimitLine("2DT") == false) {
				flag = false;
				msg += "Maximal Line 2DT : " + limitline_2dt+"\n";
				form_clear("4-3-2");
			}
		}
		if (flag) {
			switch (game.toString()) {
				case "4":
					nmgame = "4D";
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win4dnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win4dbb_kena_bet;
							break;
						default:
							diskon = bet_432 * disc4d_bet;
							diskonpercen = disc4d_bet;
							win = win4d_bet;
							break;
					}
					break;
				case "3":
					nmgame = "3D";
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win3dnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win3dbb_kena_bet;
							break;
						default:
							diskon = bet_432 * disc3d_bet;
							diskonpercen = disc3d_bet;
							win = win3d_bet;
							break;
					}
					break;
				case "3DD":
					nmgame = "3DD";
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win3ddnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win3ddbb_kena_bet;
							break;
						default:
							diskon = bet_432 * disc3dd_bet;
							diskonpercen = disc3dd_bet;
							win = win3dd_bet;
							break;
					}
					break;
				case "2":
					nmgame = "2D";
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win2dnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win2dbb_kena_bet;
							break;
						default:
							diskon = bet_432 * disc2d_bet;
							diskonpercen = disc2d_bet;
							win = win2d_bet;
							break;
					}
					break;
				case "2DD":
					nmgame = "2DD";
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win2ddnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win2ddbb_kena_bet;
							break;
						default:
							diskon = bet_432 * disc2dd_bet;
							diskonpercen = disc2dd_bet;
							win = win2dd_bet;
							break;
					}
					break;
				case "2DT":
					nmgame = "2DT";
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win2dtnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win2dtbb_kena_bet;
							break;
						default:
							diskon = bet_432 * disc2dt_bet;
							diskonpercen = disc2dt_bet;
							win = win2dt_bet;
							break;
					}
					break;
			}
			bayar = parseInt(bet_432) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;

			addKeranjang(
				nomor_432,
				nmgame,
				bet_432,
				diskonpercen,
				diskon,
				bayar,
				win,
				0,
				0,flag_fulldiskon
			);
			form_clear("4-3-2");
			if (temp_bulk_error != "") {
				let myModal = new bootstrap.Modal(
					document.getElementById("modalError")
				);
				myModal.show();
			}
		}
		if(msg != ""){
			alert(msg)
		}
	}
	function form4dset_add() {
		let flag = true;
		let flagfinish = false;
		let game = nomorset.length;
		let bet = 0;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let nomor = "";
		let msg = "";
		let code_alert = 0;
		let note_alert = "";
		if (nomorset == "") {
			nomorset_input.focus();
			flag = false;
		}
		if (parseInt(betset_1) > 0) {
			if (parseInt(betset_1) < parseInt(minimal_bet)) {
				betset_1 = minimal_bet;
				flag = false;
				msg += "Minimal Bet 4D : " +new Intl.NumberFormat().format(minimal_bet)+"\n";
			}
			if (parseInt(betset_1) > parseInt(max4d_bet)) {
				betset_1 = max4d_bet;
				flag = false;
				msg += "Maximal Bet 4D : " +new Intl.NumberFormat().format(max4d_bet)+"\n";
			}
			if (flag == true) {
				if (game.toString() == "4") {
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win4dnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win4dbb_kena_bet;
							break;
						default:
							diskon = Math.ceil(betset_1 * disc4d_bet);
							diskonpercen = disc4d_bet;
							win = win4d_bet;
							break;
					}
					bayar = parseInt(betset_1) - parseInt(Math.ceil(diskon));
					if (checkLimitLine("4D") == true) {
						nomor = nomorset;
						totalkeranjang = bayar + totalkeranjang;
						bet = betset_1;
						addKeranjang(
							nomor,
							"4D",
							bet,
							diskonpercen,
							diskon,
							bayar,
							win,
							0,
							0,flag_fulldiskon
						);
						flagfinish = true
					} else {
						code_alert = 1;
						note_alert = "Line 4D sudah melebihi limit";
					}
					if (code_alert == 1) {
						alert(note_alert);
						code_alert = 0;
					}
				}
			}
		}
		if (parseInt(betset_2) > 0) {
			if (parseInt(betset_2) < parseInt(minimal_bet)) {
				betset_2 = minimal_bet;
				flag = false;
				msg += "Minimal Bet 3D : " +new Intl.NumberFormat().format(minimal_bet)+"\n";
			}
			if (parseInt(betset_2) > parseInt(max3d_bet)) {
				betset_2 = max3d_bet;
				flag = false;
				msg += "Maximal Bet 3D : " +new Intl.NumberFormat().format(max3d_bet)+"\n";
			}
			if (flag == true) {
				if (game.toString() == "4" || game.toString() == "3") {
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win3dnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win3dbb_kena_bet;
							break;
						default:
							diskon = Math.ceil(betset_2 * disc3d_bet);
							diskonpercen = disc3d_bet;
							win = win3d_bet;
							break;
					}
					bayar = parseInt(betset_2) - parseInt(Math.ceil(diskon));
					if (checkLimitLine("3D") == true) {
						switch(game.toString()){
							case "4":
								nomor = nomorset[1]+nomorset[2]+nomorset[3];
								break;
							case "3":
								nomor = nomorset[0]+nomorset[1]+nomorset[2];
								break;
						}
						totalkeranjang = bayar + totalkeranjang;
						bet = betset_2;
						addKeranjang(
							nomor,
							"3D",
							bet,
							diskonpercen,
							diskon,
							bayar,
							win,
							0,
							0,flag_fulldiskon
						);
						flagfinish = true
					} else {
						code_alert = 1;
						note_alert = "Line 3D sudah melebihi limit";
					}

					if (code_alert == 1) {
						alert(note_alert);
						code_alert = 0;
					}
				}
			}
		}
		if (parseInt(betset_3) > 0) {
			if (parseInt(betset_3) < parseInt(minimal_bet)) {
				betset_3 = minimal_bet;
				flag = false;
				msg += "Minimal Bet 2D : " +new Intl.NumberFormat().format(minimal_bet)+"\n";
			}
			if (parseInt(betset_3) > parseInt(max2d_bet)) {
				betset_3 = max2d_bet;
				flag = false;
				msg += "Maximal Bet 2D : " +new Intl.NumberFormat().format(max2d_bet)+"\n";
			}
			if (flag == true) {
				if (game.toString() == "4" || game.toString() == "3" || game.toString() == "2") {
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win2dnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win2dbb_kena_bet;
							break;
						default:
							diskon = Math.ceil(betset_3 * disc2d_bet);
							diskonpercen = disc2d_bet;
							win = win2d_bet;
							break;
					}
					
					bayar = parseInt(betset_3) - parseInt(Math.ceil(diskon));
					if (checkLimitLine("2D") == true) {
						switch(game.toString()){
							case "4":
								nomor = nomorset[2]+nomorset[3];
								break;
							case "3":
								nomor = nomorset[1]+nomorset[2];
								break;
							case "2":
								nomor = nomorset[0]+nomorset[1];
								break;
						}
						totalkeranjang = bayar + totalkeranjang;
						bet = betset_3;
						addKeranjang(
							nomor,
							"2D",
							bet,
							diskonpercen,
							diskon,
							bayar,
							win,
							0,
							0,flag_fulldiskon
						);
						flagfinish = true
					} else {
						code_alert = 1;
						note_alert = "Line 2D sudah melebihi limit";
					}

					if (code_alert == 1) {
						alert(note_alert);
						code_alert = 0;
					}
				}
			}
		}
		if (parseInt(betset_4) > 0) {
			if (parseInt(betset_4) < parseInt(minimal_bet)) {
				betset_4 = minimal_bet;
				flag = false;
				msg += "Minimal Bet 2DD : " +new Intl.NumberFormat().format(minimal_bet)+"\n";
			}
			if (parseInt(betset_4) > parseInt(max2dd_bet)) {
				betset_4 = max2dd_bet;
				flag = false;
				msg += "Maximal Bet 2DD : " +new Intl.NumberFormat().format(max2dd_bet)+"\n";
			}
			if (flag == true) {
				if (game.toString() == "4" || game.toString() == "3" || game.toString() == "2") {
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win2ddnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win2ddbb_kena_bet;
							break;
						default:
							diskon = Math.ceil(betset_4 * disc2dd_bet);
							diskonpercen = disc2dd_bet;
							win = win2dd_bet;
							break;
					}
					
					bayar = parseInt(betset_4) - parseInt(Math.ceil(diskon));
					if (checkLimitLine("2DD") == true) {
						switch(game.toString()){
							case "4":
								nomor = nomorset[2]+nomorset[3];
								break;
							case "3":
								nomor = nomorset[1]+nomorset[2];
								break;
							case "2":
								nomor = nomorset[0]+nomorset[1];
								break;
						}
						totalkeranjang = bayar + totalkeranjang;
						bet = betset_4;
						addKeranjang(
							nomor,
							"2DD",
							bet,
							diskonpercen,
							diskon,
							bayar,
							win,
							0,
							0,flag_fulldiskon
						);
						flagfinish = true
					} else {
						code_alert = 1;
						note_alert = "Line 2DD sudah melebihi limit";
					}

					if (code_alert == 1) {
						alert(note_alert);
						code_alert = 0;
					}
				}
			}
		}
		if (parseInt(betset_5) > 0) {
			if (parseInt(betset_5) < parseInt(minimal_bet)) {
				betset_5 = minimal_bet;
				flag = false;
				msg += "Minimal Bet 2DT : " +new Intl.NumberFormat().format(minimal_bet)+"\n";
			}
			if (parseInt(betset_5) > parseInt(max2dt_bet)) {
				betset_5 = max2dt_bet;
				flag = false;
				msg += "Maximal Bet 2DT : " +new Intl.NumberFormat().format(max2dt_bet)+"\n";
			}
			if (flag == true) {
				if (game.toString() == "4" || game.toString() == "3" || game.toString() == "2") {
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win2dtnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win2dtbb_kena_bet;
							break;
						default:
							diskon = Math.ceil(betset_5 * disc2dt_bet);
							diskonpercen = disc2dt_bet;
							win = win2dt_bet;
							break;
					}
					
					bayar = parseInt(betset_5) - parseInt(Math.ceil(diskon));
					if (checkLimitLine("2DT") == true) {
						switch(game.toString()){
							case "4":
								nomor = nomorset[2]+nomorset[3];
								break;
							case "3":
								nomor = nomorset[1]+nomorset[2];
								break;
							case "2":
								nomor = nomorset[0]+nomorset[1];
								break;
						}
						totalkeranjang = bayar + totalkeranjang;
						bet = betset_5;
						addKeranjang(
							nomor,
							"2DT",
							bet,
							diskonpercen,
							diskon,
							bayar,
							win,
							0,
							0,flag_fulldiskon
						);
						flagfinish = true
					} else {
						code_alert = 1;
						note_alert = "Line 2DT sudah melebihi limit";
					}

					if (code_alert == 1) {
						alert(note_alert);
						code_alert = 0;
					}
				}
			}
		}
		if (parseInt(betset_6) > 0) {
			if (parseInt(betset_6) < parseInt(minimal_bet)) {
				betset_6 = minimal_bet;
				flag = false;
				msg += "Minimal Bet 3DD : " +new Intl.NumberFormat().format(minimal_bet)+"\n";
			}
			if (parseInt(betset_6) > parseInt(max3dd_bet)) {
				betset_6 = max3dd_bet;
				flag = false;
				msg += "Maximal Bet 3DD : " +new Intl.NumberFormat().format(max3dd_bet)+"\n";
			}
			if (flag == true) {
				if (game.toString() == "4" || game.toString() == "3") {
					switch(flag_fulldiskon){
						case "FULL":
							diskon = 0
							diskonpercen = 0
							win = win3ddnodiskon_bet;
							break;
						case "BB":
							diskon = 0
							diskonpercen = 0
							win = win3ddbb_kena_bet;
							break;
						default:
							diskon = Math.ceil(betset_6 * disc3d_bet);
							diskonpercen = disc3dd_bet;
							win = win3dd_bet;
							break;
					}
					bayar = parseInt(betset_6) - parseInt(Math.ceil(diskon));
					if (checkLimitLine("3DD") == true) {
						switch(game.toString()){
							case "4":
								nomor = nomorset[0]+nomorset[1]+nomorset[2];
								break;
							case "3":
								nomor = nomorset[0]+nomorset[1]+nomorset[2];
								break;
						}
						totalkeranjang = bayar + totalkeranjang;
						bet = betset_6;
						addKeranjang(
							nomor,
							"3DD",
							bet,
							diskonpercen,
							diskon,
							bayar,
							win,
							0,
							0,flag_fulldiskon
						);
						flagfinish = true
					} else {
						code_alert = 1;
						note_alert = "Line 3DD sudah melebihi limit";
					}

					if (code_alert == 1) {
						alert(note_alert);
						code_alert = 0;
					}
				}
			}
		}
		if(msg != ""){
			alert(msg)
		}
		if(flagfinish){
			form_clear("432SET");
		}
	}
	function formbbfs_add() {
		generate4D = [];
		generate3D = [];
		generate3DD = [];
		generate2D = [];
		generate2DD = [];
		generate2DT = [];

		data_bbfs = [];
		nol = 0;
		satu = 0;
		dua = 0;
		tiga = 0;
		empat = 0;
		lima = 0;
		enam = 0;
		tujuh = 0;
		delapan = 0;
		sembilan = 0;
		let found = false;
		let flag = true;
		let bet = 0;
		let game = nomorbbfs.length;
		let nmgame = "";
		let nomor = "";
		let code_alert = 0;
		let note_alert = "";
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let kei = 0;
		let kei_percen = 0;
		let bayar = 0;
		data_bbfs = [];
		if (nomorbbfs == "") {
			nomor_input.focus();
			flag = false;
			alert("Nomor Tidak Boleh Kosong");
		}
		if (nomorbbfs.length < 2 || nomorbbfs.length > bbfs) {
			flag = false;
			nomor_input.focus();
			alert("Nomor 2 - " + bbfs + " Digit");
		} else {
			countangkabbfs(nomorbbfs);
		}

		if (parseInt(bet_1) > 0) {
			if (parseInt(bet_1) < parseInt(minimal_bet)) {
				bet_1 = minimal_bet;
				flag = false;
				alert("Minimal Bet 4D : " + minimal_bet);
			}
			if (parseInt(bet_1) > parseInt(max4d_bet)) {
				bet_1 = max4d_bet;
				flag = false;
				alert("Maximal Bet 4D : " +new Intl.NumberFormat().format(max4d_bet));
			}
			if (flag == true) {
				switch(flag_fulldiskon){
					case "FULL":
						diskon = 0
						diskonpercen = 0
						win = win4dnodiskon_bet;
						break;
					case "BB":
						diskon = 0
						diskonpercen = 0
						win = win4dbb_kena_bet;
						break;
					default:
						diskon = Math.ceil(bet_1 * disc4d_bet);
						diskonpercen = disc4d_bet;
						win = win4d_bet;
						break;
				}
				bayar = parseInt(bet_1) - parseInt(Math.ceil(diskon));
				for (let a = 0; a < data_bbfs.length; a++) {
					for (let b = 0; b < data_bbfs.length; b++) {
						for (let c = 0; c < data_bbfs.length; c++) {
							for (let d = 0; d < data_bbfs.length; d++) {
								let dat =data_bbfs[a] +data_bbfs[b] +data_bbfs[c] +data_bbfs[d];
								if (generate4D.length > 0) {
									for (let x = 0;x < generate4D.length;x++) {
										if (dat == generate4D[x]) {
											found = true;
										}
									}
									if (found == false) {
										generate4D.push(dat);
									}
								} else {
									generate4D.push(dat);
								}
								found = false;
								dat = "";
							}
						}
					}
				}
				for (let x = 0; x < generate4D.length; x++) {
					if (checkcountangka(generate4D[x]) == true) {
						if (checkLimitLine("4D") == true) {
							nomor = generate4D[x];
							totalkeranjang = bayar + totalkeranjang;
							bet = bet_1;
							addKeranjang(
								nomor,
								"4D",
								bet,
								diskonpercen,
								diskon,
								bayar,
								win,
								0,
								0,flag_fulldiskon
							);
						} else {
							code_alert = 1;
							note_alert = "Line 4D sudah melebihi limit";
							break;
						}
					}
				}

				if (code_alert == 1) {
					alert(note_alert);
					code_alert = 0;
				}
			}
		}
		if (parseInt(bet_2) > 0) {
			if (parseInt(bet_2) < parseInt(minimal_bet)) {
				bet_2 = minimal_bet;
				flag = false;
				alert("Minimal Bet 3D : " + minimal_bet);
			}
			if (parseInt(bet_2) > parseInt(max3d_bet)) {
				bet_2 = max3d_bet;
				flag = false;
				alert("Maximal Bet 3D : " +new Intl.NumberFormat().format(max3d_bet));
			}
			if (flag == true) {
				switch(flag_fulldiskon){
					case "FULL":
						diskon = 0
						diskonpercen = 0
						win = win3dnodiskon_bet;
						break;
					case "BB":
						diskon = 0
						diskonpercen = 0
						win = win3dbb_kena_bet;
						break;
					default:
						diskon = Math.ceil(bet_2 * disc3d_bet);
						diskonpercen = disc3d_bet;
						win = win3d_bet;
						break;
				}
				bayar = parseInt(bet_2) - parseInt(Math.ceil(diskon));
				for (let a = 0; a < data_bbfs.length; a++) {
					for (let b = 0; b < data_bbfs.length; b++) {
						for (let c = 0; c < data_bbfs.length; c++) {
							let dat =
								data_bbfs[a] + data_bbfs[b] + data_bbfs[c];
							if (generate3D.length > 0) {
								for (let x = 0; x < generate3D.length; x++) {
									if (dat == generate3D[x]) {
										found = true;
									}
								}
								if (found == false) {
									generate3D.push(dat);
								}
							} else {
								generate3D.push(dat);
							}
							found = false;
							dat = "";
						}
					}
				}
				for (let x = 0; x < generate3D.length; x++) {
					if (checkcountangka(generate3D[x]) == true) {
						if (checkLimitLine("3D") == true) {
							nomor = generate3D[x];
							totalkeranjang = bayar + totalkeranjang;
							bet = bet_2;
							addKeranjang(
								nomor,
								"3D",
								bet,
								diskonpercen,
								diskon,
								bayar,
								win,
								0,
								0,flag_fulldiskon
							);
						} else {
							code_alert = 1;
							note_alert = "Line 3D sudah melebihi limit";
							break;
						}
					}
				}

				if (code_alert == 1) {
					alert(note_alert);
					code_alert = 0;
				}
			}
		}
		if (parseInt(bet_3) > 0) {
			if (parseInt(bet_3) < parseInt(minimal_bet)) {
				bet_3 = minimal_bet;
				flag = false;
				alert("Minimal Bet 2D : " + minimal_bet);
			}
			if (parseInt(bet_3) > parseInt(max2d_bet)) {
				bet_3 = max2d_bet;
				flag = false;
				alert(
					"Maximal Bet 2D : " +
						new Intl.NumberFormat().format(max2d_bet)
				);
			}
			if (flag == true) {
				switch(flag_fulldiskon){
					case "FULL":
						diskon = 0
						diskonpercen = 0
						win = win2dnodiskon_bet;
						break;
					case "BB":
						diskon = 0
						diskonpercen = 0
						win = win2dbb_kena_bet;
						break;
					default:
						diskon = Math.ceil(bet_3 * disc2d_bet);
						diskonpercen = disc2d_bet;
						win = win2d_bet;
						break;
				}
				bayar = parseInt(bet_3) - parseInt(Math.ceil(diskon));
				for (let a = 0; a < data_bbfs.length; a++) {
					for (let b = 0; b < data_bbfs.length; b++) {
						let dat = data_bbfs[a] + data_bbfs[b];
						if (generate2D.length > 0) {
							for (let x = 0; x < generate2D.length; x++) {
								if (dat == generate2D[x]) {
									found = true;
								}
							}
							if (found == false) {
								generate2D.push(dat);
							}
						} else {
							generate2D.push(dat);
						}
						found = false;
						dat = "";
					}
				}
				for (let x = 0; x < generate2D.length; x++) {
					if (checkcountangka(generate2D[x]) == true) {
						if (checkLimitLine("2D") == true) {
							nomor = generate2D[x];
							totalkeranjang = bayar + totalkeranjang;
							bet = bet_3;
							addKeranjang(
								nomor,
								"2D",
								bet,
								diskonpercen,
								diskon,
								bayar,
								win,
								0,
								0,flag_fulldiskon
							);
						} else {
							code_alert = 1;
							note_alert = "Line 2D sudah melebihi limit";
							break;
						}
					}
				}
				if (temp_bulk_error != "") {
					let myModal = new bootstrap.Modal(
						document.getElementById("modalError")
					);
					myModal.show();
				}
				if (code_alert == 1) {
					alert(note_alert);
					code_alert = 0;
				}
			}
		}
		if (parseInt(bet_4) > 0) {
			if (parseInt(bet_4) < parseInt(minimal_bet)) {
				bet_4 = minimal_bet;
				flag = false;
				alert("Minimal Bet 2DD : " + minimal_bet);
			}
			if (parseInt(bet_4) > parseInt(max2dd_bet)) {
				bet_4 = max2dd_bet;
				flag = false;
				alert("Maximal Bet 2DD : " +new Intl.NumberFormat().format(max2dd_bet));
			}
			if (flag == true) {
				switch(flag_fulldiskon){
					case "FULL":
						diskon = 0
						diskonpercen = 0
						win = win2ddnodiskon_bet;
						break;
					case "BB":
						diskon = 0
						diskonpercen = 0
						win = win2ddbb_kena_bet;
						break;
					default:
						diskon = Math.ceil(bet_4 * disc2dd_bet);
						diskonpercen = disc2dd_bet;
						win = win2dd_bet;
						break;
				}
				bayar = parseInt(bet_4) - parseInt(Math.ceil(diskon));
				for (let a = 0; a < data_bbfs.length; a++) {
					for (let b = 0; b < data_bbfs.length; b++) {
						let dat = data_bbfs[a] + data_bbfs[b];
						if (generate2DD.length > 0) {
							for (let x = 0; x < generate2DD.length; x++) {
								if (dat == generate2DD[x]) {
									found = true;
								}
							}
							if (found == false) {
								generate2DD.push(dat);
							}
						} else {
							generate2DD.push(dat);
						}
						found = false;
						dat = "";
					}
				}
				for (let x = 0; x < generate2DD.length; x++) {
					if (checkcountangka(generate2DD[x]) == true) {
						if (checkLimitLine("2DD") == true) {
							nomor = generate2DD[x];
							totalkeranjang = bayar + totalkeranjang;
							bet = bet_4;
							addKeranjang(
								nomor,
								"2DD",
								bet,
								diskonpercen,
								diskon,
								bayar,
								win,
								0,
								0,flag_fulldiskon
							);
						} else {
							code_alert = 1;
							note_alert = "Line 2DD sudah melebihi limit";
							break;
						}
					}
				}
				if (temp_bulk_error != "") {
					let myModal = new bootstrap.Modal(
						document.getElementById("modalError")
					);
					myModal.show();
				}
				if (code_alert == 1) {
					alert(note_alert);
					code_alert = 0;
				}
			}
		}
		if (parseInt(bet_5) > 0) {
			if (parseInt(bet_5) < parseInt(minimal_bet)) {
				bet_5 = minimal_bet;
				flag = false;
				alert("Minimal Bet 2DT : " + minimal_bet);
			}
			if (parseInt(bet_5) > parseInt(max2dt_bet)) {
				bet_5 = max2dt_bet;
				flag = false;
				alert("Maximal Bet 2DT : " +new Intl.NumberFormat().format(max2dt_bet));
			}
			if (flag == true) {
				switch(flag_fulldiskon){
					case "FULL":
						diskon = 0
						diskonpercen = 0
						win = win2dtnodiskon_bet;
						break;
					case "BB":
						diskon = 0
						diskonpercen = 0
						win = win2dtbb_kena_bet;
						break;
					default:
						diskon = Math.ceil(bet_5 * disc2dt_bet);
						diskonpercen = disc2dt_bet;
						win = win2dd_bet;
						break;
				}
				bayar = parseInt(bet_5) - parseInt(Math.ceil(diskon));
				for (let a = 0; a < data_bbfs.length; a++) {
					for (let b = 0; b < data_bbfs.length; b++) {
						let dat = data_bbfs[a] + data_bbfs[b];
						if (generate2DT.length > 0) {
							for (let x = 0; x < generate2DT.length; x++) {
								if (dat == generate2DT[x]) {
									found = true;
								}
							}
							if (found == false) {
								generate2DT.push(dat);
							}
						} else {
							generate2DT.push(dat);
						}
						found = false;
						dat = "";
					}
				}
				for (let x = 0; x < generate2DT.length; x++) {
					if (checkcountangka(generate2DT[x]) == true) {
						if (checkLimitLine("2DT") == true) {
							nomor = generate2DT[x];
							totalkeranjang = bayar + totalkeranjang;
							bet = bet_5;
							addKeranjang(
								nomor,
								"2DT",
								bet,
								diskonpercen,
								diskon,
								bayar,
								win,
								0,
								0,flag_fulldiskon
							);
						} else {
							code_alert = 1;
							note_alert = "Line 2DT sudah melebihi limit";
							break;
						}
					}
				}
				if (temp_bulk_error != "") {
					let myModal = new bootstrap.Modal(
						document.getElementById("modalError")
					);
					myModal.show();
				}
				if (code_alert == 1) {
					alert(note_alert);
					code_alert = 0;
				}
			}
		}
		if (parseInt(bet_6) > 0) {
			if (parseInt(bet_6) < parseInt(minimal_bet)) {
				bet_6 = minimal_bet;
				flag = false;
				alert("Minimal Bet 3DD : " + minimal_bet);
			}
			if (parseInt(bet_6) > parseInt(max3dd_bet)) {
				bet_6 = max3dd_bet;
				flag = false;
				alert("Maximal Bet 3DD : " +new Intl.NumberFormat().format(max3dd_bet));
			}
			if (flag == true) {
				switch(flag_fulldiskon){
					case "FULL":
						diskon = 0
						diskonpercen = 0
						win = win3ddnodiskon_bet;
						break;
					case "BB":
						diskon = 0
						diskonpercen = 0
						win = win3ddbb_kena_bet;
						break;
					default:
						diskon = Math.ceil(bet_6 * disc3dd_bet);
						diskonpercen = disc3dd_bet;
						win = win3dd_bet;
						break;
				}
				bayar = parseInt(bet_6) - parseInt(Math.ceil(diskon));
				for (let a = 0; a < data_bbfs.length; a++) {
					for (let b = 0; b < data_bbfs.length; b++) {
						for (let c = 0; c < data_bbfs.length; c++) {
							let dat = data_bbfs[a] + data_bbfs[b] + data_bbfs[c];
							if (generate3DD.length > 0) {
								for (let x = 0; x < generate3DD.length; x++) {
									if (dat == generate3DD[x]) {
										found = true;
									}
								}
								if (found == false) {
									generate3DD.push(dat);
								}
							} else {
								generate3DD.push(dat);
							}
							found = false;
							dat = "";
						}
					}
				}
				for (let x = 0; x < generate3DD.length; x++) {
					if (checkcountangka(generate3DD[x]) == true) {
						if (checkLimitLine("3DD") == true) {
							nomor = generate3DD[x];
							totalkeranjang = bayar + totalkeranjang;
							bet = bet_6;
							addKeranjang(
								nomor,
								"3DD",
								bet,
								diskonpercen,
								diskon,
								bayar,
								win,
								0,
								0,flag_fulldiskon
							);
						} else {
							code_alert = 1;
							note_alert = "Line 3DD sudah melebihi limit";
							break;
						}
					}
				}

				if (code_alert == 1) {
					alert(note_alert);
					code_alert = 0;
				}
			}
		}
		form_clear("bbfs");
	}
	function form3dd_add() {
		let flag = true;
		let game = nomor3dd.length;
		let bet = 0;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let nomor = "";
		let nmgame = "";
		let msg_error = ""
		if (nomor3dd == "") {
			nomor3dd_input.focus();
			flag = false;
		}
		if (bet_3dd == "") {
			flag = false;
			msg_error += "Bet tidak boleh kosong";
		}
		if (parseInt(bet_3dd) < parseInt(minimal_bet)) {
			bet_3dd = minimal_bet;
			flag = false;
			msg_error += "Minimal Bet : " + minimal_bet;
		}

		if (game.toString() == "3") {
			if (parseInt(bet_3dd) > parseInt(max3dd_bet)) {
				bet_3dd = minimal_bet;
				flag = false;
				msg_error += "Maximal Bet 3D Depan : " + max3dd_bet;
			}
			if (checkLimitLine("3DD") == false) {
				flag = false;
				msg_error += "Maximal Line 3D Depan : " + limitline_3dd;
				form_clear("3DD");
			}
		}else{
			flag = false;
			msg_error += "Minimal 3 Digit";
			form_clear("3DD");
		}

		for (var i = 0; i < nomor3dd.length; i++) {
			let numbera = parseInt(nomor3dd[i]);
			if (isNaN(numbera)) {
				flag = false;
				msg_error +="Nomor harus angka";
				form_clear("3DD");
			}
		}
		
		if (flag == true) {
			nmgame = "3DD";
			switch(flag_fulldiskon){
				case "FULL":
					diskon = 0
					diskonpercen = 0
					win = win3ddnodiskon_bet;
					break;
				case "BB":
					diskon = 0
					diskonpercen = 0
					win = win3ddbb_kena_bet;
					break;
				default:
					diskon = bet_3dd * disc3dd_bet;
					diskonpercen = disc3dd_bet;
					win = win3dd_bet;
					break;
			}
			
			nomor = nomor3dd;
			bet = bet_3dd;
			bayar = parseInt(bet_3dd) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;
			addKeranjang(
				nomor,
				nmgame,
				bet,
				diskonpercen,
				diskon,
				bayar,
				win,
				0,
				0,flag_fulldiskon
			);
			form_clear("3DD");
		}
		if(msg_error != ""){
			alert(msg_error)
		}
	}
	function form2dd_add() {
		let flag = true;
		let game = nomor2dd.length;
		let bet = 0;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let kei = 0;
		let kei_percen = 0;
		let bayar = 0;
		let nmgame = "";
		let nomor = "";
		if (nomor2dd == "") {
			nomor2dd_input.focus();
			flag = false;
		}

		if (bet_2dd == "") {
			flag = false;
			alert("Bet tidak boleh kosong");
		}
		if (parseInt(bet_2dd) < parseInt(minimal_bet)) {
			bet_2dd = minimal_bet;
			flag = false;
			alert("Minimal Bet : " + minimal_bet);
		}

		if (game.toString() == "2") {
			if (parseInt(bet_2dd) > parseInt(max2dd_bet)) {
				bet_2dd = minimal_bet;
				flag = false;
				alert("Maximal Bet 2D Depan : " + max2dd_bet);
			}
			if (checkLimitLine("2DD") == false) {
				flag = false;
				alert("Maximal Line 2D Depan : " + limitline_2dd);
				form_clear("2DD");
			}
		}else{
			flag = false;
			alert("Minimal 2 Digit");
			form_clear("2DD");
		}

		for (var i = 0; i < nomor2dd.length; i++) {
			let numbera = parseInt(nomor2dd[i]);
			if (isNaN(numbera)) {
				flag = false;
				alert("Error");
				form_clear("2DD");
			}
		}
		if (flag == true) {
			nmgame = "2DD";
			switch(flag_fulldiskon){
				case "FULL":
					diskon = 0
					diskonpercen = 0
					win = win2ddnodiskon_bet;
					break;
				case "BB":
					diskon = 0
					diskonpercen = 0
					win = win2ddbb_kena_bet;
					break;
				default:
					diskon = bet_2dd * disc2dd_bet;
					diskonpercen = disc2dd_bet;
					win = win2dd_bet;
					break;
			}
			
			nomor = nomor2dd;
			bet = bet_2dd;
			bayar = parseInt(bet_2dd) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;
			addKeranjang(
				nomor,
				nmgame,
				bet,
				diskonpercen,
				diskon,
				bayar,
				win,
				0,
				0,flag_fulldiskon
			);
			form_clear("2DD");
		}
		if (temp_bulk_error != "") {
			let myModal = new bootstrap.Modal(
				document.getElementById("modalError")
			);
			myModal.show();
		}
	}
	function form2dt_add() {
		let flag = true;
		let game = nomor2dt.length;
		let bet = 0;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let kei = 0;
		let kei_percen = 0;
		let bayar = 0;
		let nmgame = "";
		let nomor = "";
		if (nomor2dt == "") {
			nomor2dt_input.focus();
			flag = false;
		}

		if (bet_2dt == "") {
			flag = false;
			alert("Bet tidak boleh kosong");
		}
		if (parseInt(bet_2dt) < parseInt(minimal_bet)) {
			bet_2dt = minimal_bet;
			flag = false;
			alert("Minimal Bet : " + minimal_bet);
		}

		if (game.toString() == "2") {
			if (parseInt(bet_2dt) > parseInt(max2dt_bet)) {
				bet_2dt = minimal_bet;
				flag = false;
				alert("Maximal Bet 2D Tengah : " + max2dt_bet);
			}
			if (checkLimitLine("2DT") == false) {
				flag = false;
				alert("Maximal Line 2T Tengah : " + limitline_2dd);
				form_clear("2DT");
			}
		}else{
			flag = false;
			alert("Minimal 2 Digit");
			form_clear("2DD");
		}

		for (var i = 0; i < nomor2dt.length; i++) {
			let numbera = parseInt(nomor2dt[i]);
			if (isNaN(numbera)) {
				flag = false;
				alert("Error");
				form_clear("2DT");
			}
		}
		if (flag == true) {
			nmgame = "2DT";
			switch(flag_fulldiskon){
				case "FULL":
					diskon = 0
					diskonpercen = 0
					win = win2dtnodiskon_bet;
					break;
				case "BB":
					diskon = 0
					diskonpercen = 0
					win = win2dtbb_kena_bet;
					break;
				default:
					diskon = bet_2dt * disc2dt_bet;
					diskonpercen = disc2dt_bet;
					win = win2dt_bet;
					break;
			}
			
			nomor = nomor2dt;
			bet = bet_2dt;
			bayar = parseInt(bet_2dt) - parseInt(Math.ceil(diskon));
			totalkeranjang = bayar + totalkeranjang;
			addKeranjang(
				nomor,
				nmgame,
				bet,
				diskonpercen,
				diskon,
				bayar,
				win,
				0,
				0,flag_fulldiskon
			);
			form_clear("2DT");
		}
		if (temp_bulk_error != "") {
			let myModal = new bootstrap.Modal(
				document.getElementById("modalError")
			);
			myModal.show();
		}
	}
	function formwap_add() {
		let pemisah = nomorwap.split(",");
		let res_money = nomorwap.split("#");
		let totalpemisah = pemisah.length;
		let totalres_money = res_money.length;
		let flag_checkdata = true;
		for (let i = 0; i < nomorwap.length; i++) {
			let numbera = parseInt(nomorwap[i]);
			if (isNaN(numbera)) {
				if (nomorwap[i] != "*" && nomorwap[i] != "#" && nomorwap[i] != ",") {
					form_clear("wap");
					flag_checkdata = false;
				}
			}
		}
		if (flag_checkdata == false) {
			alert("Format Salah, hanya boleh karakter angka * # ,");
		} else {
			if (totalpemisah < 2) {
				//jika tidak ada pemisah
				if (totalres_money < 2) {
					alert("Format Salah");
				} else {
					checkbulkdata(nomorwap);
				}
			} else {
				for (var i = 0; i < totalpemisah; i++) {
					checkbulkdata(pemisah[i]);
				}
			}
		}
		if (temp_bulk_error != "") {
			let myModal = new bootstrap.Modal(
				document.getElementById("modalError")
			);
			myModal.show();
		}
	}
	function formpolatarung_add() {
		let flag = true;
		let nomoras_game = nomoras.length;
		let nomorkop_game = nomorkop.length;
		let nomorkepala_game = nomorkepala.length;
		let nomorekor_game = nomorekor.length;
		let pola = ""
		let count = 0
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let bayar = 0;
		let msg = "";
		if (nomoras == "") {
			nomoras_input.focus();
			flag = false;
			pola += "-"
		}else{
			pola += "1"
		}
		if (nomorkop == "") {
			nomorkop_input.focus();
			flag = false;
			pola += "-"
		}else{
			pola += "1"
		}
		if (nomorkepala != "") {
			pola += "1"
		}else{
			pola += "-"
		}
		if (nomorekor != "") {
			pola += "1"
		}else{
			pola += "-"
		}
		if(bet_tarung == ""){
			bet_tarung_input.focus();
			msg += "Bet Wajib diisi"
			flag = false;
		}
		if (parseInt(bet_tarung) < parseInt(minimal_bet)) {
			bet_tarung = minimal_bet;
			flag = false;
			msg += "Minimal Bet : " + minimal_bet;
		}

		if (flag) {
			let nomor = ""
			switch(pola){
				case "11--":
					for(let i=0;i<nomoras_game;i++){
						for(let j=0;j<nomorkop_game;j++){
							if (checkLimitLine("2D") == true) {
								nomor = nomoras[i] + nomorkop[j]
								count = count + 1
								switch(flag_fulldiskon){
									case "FULL":
										diskon = 0
										diskonpercen = 0
										win = win2dnodiskon_bet;
										break;
									case "BB":
										diskon = 0
										diskonpercen = 0
										win = win2dbb_kena_bet;
										break;
									default:
										diskon = bet_tarung * disc2d_bet;
										diskonpercen = disc2d_bet;
										win = win2d_bet;
										break;
								}
								
								bayar = parseInt(bet_tarung) - parseInt(Math.ceil(diskon));
								totalkeranjang = bayar + totalkeranjang;
								addKeranjang(
									nomor,
									"2D",
									bet_tarung,
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
					form_clear("polatarung");
				break;
				case "111-":
					for(let i=0;i<nomoras_game;i++){
						for(let j=0;j<nomorkop_game;j++){
							for(let x=0;x<nomorkepala_game;x++){
								if (checkLimitLine("3D") == true) {
									nomor = nomoras[i]+nomorkop[j]+nomorkepala[x]
									count = count + 1
									switch(flag_fulldiskon){
										case "FULL":
											diskon = 0
											diskonpercen = 0
											win = win3dnodiskon_bet;
											break;
										case "BB":
											diskon = 0
											diskonpercen = 0
											win = win3dbb_kena_bet;
											break;
										default:
											diskon = bet_tarung * disc3d_bet;
											diskonpercen = disc3d_bet;
											win = win3d_bet;
											break;
									}
									
									bayar = parseInt(bet_tarung) - parseInt(Math.ceil(diskon));
									totalkeranjang = bayar + totalkeranjang;
									addKeranjang(
										nomor,
										"3D",
										bet_tarung,
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
					}
					form_clear("polatarung");
				break;
				case "1111":
					for(let i=0;i<nomoras_game;i++){
						for(let j=0;j<nomorkop_game;j++){
							for(let x=0;x<nomorkepala_game;x++){
								for(let y=0;y<nomorekor_game;y++){
									if (checkLimitLine("4D") == true) {
										nomor = nomoras[i]+nomorkop[j]+nomorkepala[x]+nomorekor[y]
										count = count + 1
										switch(flag_fulldiskon){
											case "FULL":
												diskon = 0
												diskonpercen = 0
												win = win4dnodiskon_bet;
												break;
											case "BB":
												diskon = 0
												diskonpercen = 0
												win = win4dbb_kena_bet;
												break;
											default:
												diskon = bet_tarung * disc4d_bet;
												diskonpercen = disc4d_bet;
												win = win4d_bet;
												break;
										}
										
										bayar = parseInt(bet_tarung) - parseInt(Math.ceil(diskon));
										totalkeranjang = bayar + totalkeranjang;
										addKeranjang(
											nomor,
											"4D",
											bet_tarung,
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
						}
					}
					form_clear("polatarung");
					break;
				default:
					msg = "Format Pola Tarung Salah"
				break;
			}
		}
		if(msg != ""){
			alert(msg)
			form_clear("polatarung")
		}
	}
	function formquick2d_add() {
		let flag = true;
		let diskon = 0;
		let diskonpercen = 0;
		let bet = 0;
		let win = 0;
		let kei = 0;
		let kei_percen = 0;
		let bayar = 0;
		let nmgame = "";
		let data_temp = [];
		let data_quick = [];
		let code_alert = 0;
		let note_alert = "";
		if (quick_pilihan1 == "") {
			quick_pilihan1_input.focus();
			flag = false;
			alert("Besar/Kecil/Genap/Ganjil tidak boleh kosong");
		}
		if (quick_pilihan2 == "") {
			quick_pilihan2_input.focus();
			flag = false;
			alert("2D/2D Depan/2D Tengah tidak boleh kosong");
		}
		if (quick_bet == "") {
			quick_bet_input.focus();
			flag = false;
			alert("Bet tidak boleh kosong");
		}
		if (parseInt(quick_bet) < parseInt(minimal_bet)) {
			quick_bet = minimal_bet;
			flag = false;
			alert("Minimal Bet : " + minimal_bet);
		}
		if (quick_pilihan2 != "") {
			switch (quick_pilihan2) {
				case "2D":
					if (parseInt(quick_bet) > parseInt(max2d_bet)) {
						quick_bet = minimal_bet;
						flag = false;
						alert("Maximal Bet 2D  : " + max2d_bet);
					}
					break;
				case "2DD":
					if (parseInt(quick_bet) > parseInt(max2dd_bet)) {
						quick_bet = minimal_bet;
						flag = false;
						alert("Maximal Bet 2D Depan : " + max2dd_bet);
					}
					break;
				case "2DT":
					if (parseInt(quick_bet) > parseInt(max2dt_bet)) {
						quick_bet = minimal_bet;
						flag = false;
						alert("Maximal Bet 2D Tengah : " + max2dt_bet);
					}
					break;
			}
		}

		if (flag == true) {
			for (let x = 0; x < 10; x++) {
				for (let y = 0; y < 10; y++) {
					data_temp.push(x.toString() + y.toString());
				}
			}
			if (data_temp.length > 0) {
				switch (quick_pilihan1) {
					case "BESAR":
						for (let i = 0; i <= data_temp.length; i++) {
							if (parseInt(data_temp[i]) > 49) {
								data_quick.push(data_temp[i]);
							}
						}
						break;
					case "KECIL":
						for (let i = 0; i <= data_temp.length; i++) {
							if (parseInt(data_temp[i]) < 50) {
								data_quick.push(data_temp[i]);
							}
						}
						break;
					case "GANJIL":
						for (let i = 0; i < data_temp.length; i++) {
							if (parseInt(data_temp[i]) % 2 !== 0) {
								data_quick.push(data_temp[i]);
							}
						}
						break;
					case "GENAP":
						for (let i = 0; i < data_temp.length; i++) {
							if (parseInt(data_temp[i]) % 2 == 0) {
								data_quick.push(data_temp[i]);
							}
						}
						break;
				}
			}
			if (data_quick.length > 0) {
				switch (quick_pilihan2) {
					case "2D":
						bet = quick_bet;
						nmgame = "2D";
						switch(flag_fulldiskon){
							case "FULL":
								diskon = 0
								diskonpercen = 0
								win = win2dnodiskon_bet;
								break;
							case "BB":
								diskon = 0
								diskonpercen = 0
								win = win2dbb_kena_bet;
								break;
							default:
								diskon = quick_bet * disc2d_bet;
								diskonpercen = disc2d_bet;
								win = win2d_bet;
								break;
						}
						
						bayar = parseInt(quick_bet) - parseInt(Math.ceil(diskon));
						for (let i = 0; i < data_quick.length; i++) {
							if (checkLimitLine("2D") == false) {
								code_alert = 1;
								note_alert = "Line 2D sudah melebihi limit";
								break;
							} else {
								totalkeranjang = bayar + totalkeranjang;
								addKeranjang(
									data_quick[i],
									nmgame,
									bet,
									diskonpercen,
									diskon,
									bayar,
									win,
									0,
									0,flag_fulldiskon
								);
								form_clear("quick2D");
							}
						}
						if (code_alert == 1) {
							alert(note_alert);
							code_alert = 0;
						}
						if (temp_bulk_error != "") {
							let myModal = new bootstrap.Modal(
								document.getElementById("modalError")
							);
							myModal.show();
						}
						break;
					case "2DD":
						bet = quick_bet;
						nmgame = "2DD";
						switch(flag_fulldiskon){
							case "FULL":
								diskon = 0
								diskonpercen = 0
								win = win2ddnodiskon_bet;
								break;
							case "BB":
								diskon = 0
								diskonpercen = 0
								win = win2ddbb_kena_bet;
								break;
							default:
								diskon = quick_bet * disc2dd_bet;
								diskonpercen = disc2dd_bet;
								win = win2dd_bet;
								break;
						}
						
						bayar = parseInt(quick_bet) - parseInt(Math.ceil(diskon));
						for (let i = 0; i < data_quick.length; i++) {
							if (checkLimitLine("2DD") == false) {
								code_alert = 1;
								note_alert = "Line 2DD sudah melebihi limit";
								break;
							} else {
								totalkeranjang = bayar + totalkeranjang;
								const data = {
									id: Math.floor(Math.random() * 5000) + 3,
									nomor: data_quick[i],
									permainan: nmgame,
									bet,
									diskon,
									diskonpercen,
									bayar,
									win,
									kei,
									kei_percen,
								};
								addKeranjang(
									data_quick[i],
									nmgame,
									bet,
									diskonpercen,
									diskon,
									bayar,
									win,
									0,
									0,flag_fulldiskon
								);
								form_clear("quick2D");
							}
						}
						if (code_alert == 1) {
							alert(note_alert);
							code_alert = 0;
						}
						if (temp_bulk_error != "") {
							let myModal = new bootstrap.Modal(
								document.getElementById("modalError")
							);
							myModal.show();
						}
						break;
					case "2DT":
						bet = quick_bet;
						nmgame = "2DT";
						switch(flag_fulldiskon){
							case "FULL":
								diskon = 0
								diskonpercen = 0
								win = win2dtnodiskon_bet;
								break;
							case "BB":
								diskon = 0
								diskonpercen = 0
								win = win2dtbb_kena_bet;
								break;
							default:
								diskon = quick_bet * disc2dt_bet;
								diskonpercen = disc2dt_bet;
								win = win2dt_bet;
								break;
						}
						
						bayar = parseInt(quick_bet) - parseInt(Math.ceil(diskon));
						for (let i = 0; i < data_quick.length; i++) {
							if (checkLimitLine("2DT") == false) {
								code_alert = 1;
								note_alert = "Line 2DT sudah melebihi limit";
								break;
							} else {
								totalkeranjang = bayar + totalkeranjang;
								addKeranjang(
									data_quick[i],
									nmgame,
									bet,
									diskonpercen,
									diskon,
									bayar,
									win,
									0,
									0,flag_fulldiskon
								);
								form_clear("quick2D");
							}
						}
						if (code_alert == 1) {
							alert(note_alert);
							code_alert = 0;
						}
						if (temp_bulk_error != "") {
							let myModal = new bootstrap.Modal(
								document.getElementById("modalError")
							);
							myModal.show();
						}
						break;
				}
				form_clear("quick2D");
			}
		}
	}
	function checkbulkdata(datatot) {
		let res_money = datatot.split("#");
		let flag_checkcharacter = false;
		let flag_running = false;
		let count_checkcharacter = 0;
		let money = res_money[1];
		let bet = 0;
		let datanomor = res_money[0];
		let resnomor = datanomor.split("*");
		let total_resnomor = resnomor.length;
		let diskon = 0;
		let diskonpercen = 0;
		let win = 0;
		let kei = 0;
		let kei_percen = 0;
		let bayar = 0;
		let nmgame = "";
		for (let i = 0; i < datanomor.length; i++) {
			if (datanomor[i] == "*") {
				flag_checkcharacter = true;
				count_checkcharacter = count_checkcharacter + 1;
			}
		}
		if (flag_checkcharacter == true && count_checkcharacter > 0) {
			flag_running = true;
		}
		if (flag_running == false) {
			let flag_checkdata = true;
			
			flag_checkdata = checkdata_432d(datanomor, datanomor.length, money);
			
			if (flag_checkdata == true) {
				let flag_push = false;
				let game = datanomor.length;
				
				switch (game.toString()) {
					case "4":
						if (checkLimitLine("4D") == true) {
							nmgame = "4D";
							switch(flag_fulldiskon){
								case "FULL":
									diskon = 0
									diskonpercen = 0
									win = win4dnodiskon_bet;
									break;
								case "BB":
									diskon = 0
									diskonpercen = 0
									win = win4dbb_kena_bet;
									break;
								default:
									diskon = money * disc4d_bet;
									diskonpercen = disc4d_bet;
									win = win4d_bet;
									break;
							}
							
							flag_push = true;
						}
						break;
					case "3":
						if (checkLimitLine("3D") == true) {
							nmgame = "3D";
							switch(flag_fulldiskon){
								case "FULL":
									diskon = 0
									diskonpercen = 0
									win = win3dnodiskon_bet;
									break;
								case "BB":
									diskon = 0
									diskonpercen = 0
									win = win3dbb_kena_bet;
									break;
								default:
									diskon = money * disc3d_bet;
									diskonpercen = disc3d_bet;
									win = win3d_bet;
									break;
							}
							
							flag_push = true;
						}
						break;
					case "2":
						if (checkLimitLine("2D") == true) {
							nmgame = "2D";
							switch(flag_fulldiskon){
								case "FULL":
									diskon = 0
									diskonpercen = 0
									win = win2dnodiskon_bet;
									break;
								case "BB":
									diskon = 0
									diskonpercen = 0
									win = win2dbb_kena_bet;
									break;
								default:
									diskon = money * disc2d_bet;
									diskonpercen = disc2d_bet;
									win = win2d_bet;
									break;
							}
							flag_push = true;
						}
						break;
				}
				if (flag_push == true) {
					bet = money;
					bayar = parseInt(bet) - parseInt(Math.ceil(diskon));
					totalkeranjang = bayar + totalkeranjang;
					addKeranjang(
						datanomor,
						nmgame,
						bet,
						diskonpercen,
						diskon,
						bayar,
						win,
						0,
						0,flag_fulldiskon
					);
					form_clear("wap");
				}
			}
		} else {
			for (let i = 0; i < total_resnomor; i++) {
				let nomor = resnomor[i];
				let game = resnomor[i].length;
				let flag = true;

				flag = checkdata_432d(nomor, game, money);
				if (flag == true) {
					let flag_push = false;
					switch (game.toString()) {
						case "4":
							if (checkLimitLine("4D") == true) {
								nmgame = "4D";
								switch(flag_fulldiskon){
									case "FULL":
										diskon = 0
										diskonpercen = 0
										win = win4dnodiskon_bet;
										break;
									case "BB":
										diskon = 0
										diskonpercen = 0
										win = win4dbb_kena_bet;
										break;
									default:
										diskon = money * disc4d_bet;
										diskonpercen = disc4d_bet;
										win = win4d_bet;
										break;
								}
								flag_push = true;
							}
							break;
						case "3":
							if (checkLimitLine("3D") == true) {
								nmgame = "3D";
								switch(flag_fulldiskon){
									case "FULL":
										diskon = 0
										diskonpercen = 0
										win = win3dnodiskon_bet;
										break;
									case "BB":
										diskon = 0
										diskonpercen = 0
										win = win3dbb_kena_bet;
										break;
									default:
										diskon = money * disc3d_bet;
										diskonpercen = disc3d_bet;
										win = win3d_bet;
										break;
								}
								flag_push = true;
							}
							break;
						case "2":
							if (checkLimitLine("2D") == true) {
								nmgame = "2D";
								switch(flag_fulldiskon){
									case "FULL":
										diskon = 0
										diskonpercen = 0
										win = win2dnodiskon_bet;
										break;
									case "BB":
										diskon = 0
										diskonpercen = 0
										win = win2dbb_kena_bet;
										break;
									default:
										diskon = money * disc2d_bet;
										diskonpercen = disc2d_bet;
										win = win2d_bet;
										break;
								}
								
								flag_push = true;
							}
							break;
					}
					if (flag_push == true) {
						bet = money;
						bayar = parseInt(bet) - parseInt(Math.ceil(diskon));
						totalkeranjang = bayar + totalkeranjang;

						addKeranjang(
							nomor,
							nmgame,
							bet,
							diskonpercen,
							diskon,
							bayar,
							win,
							0,
							0,flag_fulldiskon
						);

						form_clear("wap");
					}
				}
			}
		}
	}
	function checkdata_432d(nomor, game, money) {
		let flag = true;
		if (money == undefined) {
			flag = false;
		} else {
			if (parseInt(money) < parseInt(minimal_bet)) {
				form_clear("wap");
				flag = false;
				temp_bulk_error +=
					"Data Tidak Valid: " +
					nomor +
					"-" +
					game +
					"D-" +
					money +
					" | Minimal Bet : " +
					new Intl.NumberFormat().format(minimal_bet) +
					"<br />";
			}
			if (parseInt(nomor.length) < 2 || parseInt(nomor.length) > 4) {
				flag = false;
				form_clear("wap");
				temp_bulk_error +=
					"Data Tidak Valid: " +
					nomor +
					"-" +
					game +
					"D-" +
					money +
					" | Nomor harus 2 - 4 Digit<br />";
			}

			if (game.toString() == "4") {
				if (parseInt(money) > parseInt(max4d_bet)) {
					form_clear("wap");
					flag = false;
					temp_bulk_error +=
						"Data Tidak Valid: " +
						nomor +
						"-" +
						game +
						"D-" +
						money +
						" | Maximal Bet 4D : " +
						max4d_bet +
						"<br />";
				}

				if (
					parseInt(count_line_4d) +
						parseInt(db_form4d_4d_count_temp) >=
					parseInt(limitline_4d)
				) {
					flag = false;
				}
			}
			if (game.toString() == "3") {
				if (parseInt(money) > parseInt(max3d_bet)) {
					form_clear("wap");
					flag = false;
				}
				if (
					parseInt(count_line_3d) +
						parseInt(db_form4d_3d_count_temp) >
					parseInt(limitline_3d)
				) {
					flag = false;
				}
			}
			if (game.toString() == "2") {
				if (parseInt(money) > parseInt(max2d_bet)) {
					form_clear("wap");
					flag = false;
					temp_bulk_error +=
						"Data Tidak Valid: " +
						nomor +"-" +game +"D-" +money +" | Maximal Bet 2D : " +
						new Intl.NumberFormat().format(max2d_bet) +
						"<br />";
				}
				if (
					parseInt(count_line_2d) +
						parseInt(db_form4d_2d_count_temp) >=
					parseInt(limitline_2d)
				) {
					flag = false;
				}
			}
		}

		return flag;
	}
	function checkLimitLine(game) {
		let flag = false;
		let limit4d = 0;
		let limit3d = 0;
		let limit3dd = 0;
		let limit2d = 0;
		let limit2dd = 0;
		let limit2dt = 0;
		switch (game.toString()) {
			case "4D":
				limit4d = parseInt(count_line_4d);
				if (parseInt(limit4d) < parseInt(limitline_4d)) {
					flag = true;
				}
				break;
			case "3D":
				limit3d = parseInt(count_line_3d);
				if (parseInt(limit3d) < parseInt(limitline_3d)) {
					flag = true;
				}
				break;
			case "3DD":
				limit3dd = parseInt(count_line_3dd);
				if (parseInt(limit3dd) < parseInt(limitline_3dd)) {
					flag = true;
				}
				break;
			case "2D":
				limit2d = parseInt(count_line_2d);
				if (parseInt(limit2d) < parseInt(limitline_2d)) {
					flag = true;
				}
				break;
			case "2DD":
				limit2dd = parseInt(count_line_2dd);
				if (parseInt(limit2dd) < parseInt(limitline_2dd)) {
					flag = true;
				}
				break;
			case "2DT":
				limit2dt = parseInt(count_line_2dt);
				if (parseInt(limit2dt) < parseInt(limitline_2dt)) {
					flag = true;
				}
				break;
		}

		return flag;
	}
	function countangkabbfs(x) {
		for (let i = 0; i < x.length; i++) {
			data_bbfs.push(x[i]);
			switch (x[i]) {
				case "0":
					nol = nol + 1;
					break;
				case "1":
					satu = satu + 1;
					break;
				case "2":
					dua = dua + 1;
					break;
				case "3":
					tiga = tiga + 1;
					break;
				case "4":
					empat = empat + 1;
					break;
				case "5":
					lima = lima + 1;
					break;
				case "6":
					enam = enam + 1;
					break;
				case "7":
					tujuh = tujuh + 1;
					break;
				case "8":
					delapan = delapan + 1;
					break;
				case "9":
					sembilan = sembilan + 1;
					break;
			}
		}
	}
	function checkcountangka(x) {
		//TEMP
		let nol_temp = 0;
		let satu_temp = 0;
		let dua_temp = 0;
		let tiga_temp = 0;
		let empat_temp = 0;
		let lima_temp = 0;
		let enam_temp = 0;
		let tujuh_temp = 0;
		let delapan_temp = 0;
		let sembilan_temp = 0;
		let flag = true;
		for (let i = 0; i < x.length; i++) {
			switch (x[i]) {
				case "0":
					nol_temp = nol_temp + 1;
					break;
				case "1":
					satu_temp = satu_temp + 1;
					break;
				case "2":
					dua_temp = dua_temp + 1;
					break;
				case "3":
					tiga_temp = tiga_temp + 1;
					break;
				case "4":
					empat_temp = empat_temp + 1;
					break;
				case "5":
					lima_temp = lima_temp + 1;
					break;
				case "6":
					enam_temp = enam_temp + 1;
					break;
				case "7":
					tujuh_temp = tujuh_temp + 1;
					break;
				case "8":
					delapan_temp = delapan_temp + 1;
					break;
				case "9":
					sembilan_temp = sembilan_temp + 1;
					break;
			}
		}
		if (nol_temp > nol) {
			flag = false;
		}
		if (satu_temp > satu) {
			flag = false;
		}
		if (dua_temp > dua) {
			flag = false;
		}
		if (tiga_temp > tiga) {
			flag = false;
		}
		if (empat_temp > empat) {
			flag = false;
		}
		if (lima_temp > lima) {
			flag = false;
		}
		if (enam_temp > enam) {
			flag = false;
		}
		if (tujuh_temp > tujuh) {
			flag = false;
		}
		if (delapan_temp > delapan) {
			flag = false;
		}
		if (sembilan_temp > sembilan) {
			flag = false;
		}
		return flag;
	}
	let idmodal = "";
	let myModal
	const handleTambah = (e,path) => {
		let flag = true;
		switch (e) {
			case "4-3-2":
				if (nomor_432 == "" && parseInt(bet_432) < minimal_bet) {
					nomor_432_input.focus();
				} else {
					form4d_add();
				}
				break;
			case "432SET":
				if (nomorset == "") {
					nomorset_input.focus();
				} else {
					if (isNaN(nomorset)) {
						nomorset = "";
						flag = false;
					}
					if (isNaN(betset_1)) {
						betset_1 = 0;
						flag = false;
					}
					if (isNaN(betset_2)) {
						betset_2 = 0;
						flag = false;
					}
					if (isNaN(betset_3)) {
						betset_3 = 0;
						flag = false;
					}
					if (isNaN(betset_4)) {
						betset_4 = 0;
						flag = false;
					}
					if (isNaN(betset_5)) {
						betset_5 = 0;
						flag = false;
					}
					if (flag) {
						form4dset_add();
					}
				}
				break;
			case "BBFS":
				if (nomorbbfs == "") {
					nomorbbfs_input.focus();
				} else {
					if (isNaN(nomorbbfs)) {
						nomorbbfs = "";
						flag = false;
					}
					if (isNaN(bet_1)) {
						bet_1 = 0;
						flag = false;
					}
					if (isNaN(bet_2)) {
						bet_2 = 0;
						flag = false;
					}
					if (isNaN(bet_3)) {
						bet_3 = 0;
						flag = false;
					}
					if (isNaN(bet_4)) {
						bet_4 = 0;
						flag = false;
					}
					if (isNaN(bet_5)) {
						bet_5 = 0;
						flag = false;
					}
					if (flag) {
						formbbfs_add();
					}
				}
				break;
			case "wap":
				if (nomorwap == "") {
					nomorwap_input.focus();
				} else {
					formwap_add();
				}
				break;
			case "polatarung":
				if (nomoras == "") {
					nomoras_input.focus();
					flag = false
				} 
				if (nomorkop == "") {
					nomorkop_input.focus();
					flag = false
				} 
				if(flag){
					formpolatarung_add();
				}
				break;
			case "3DD":
				if (nomor3dd == "" && parseInt(bet_3dd) < minimal_bet) {
					nomor3dd_input.focus();
				} else {
					if (nomor3dd.length < 3){
						nomor3dd = "";
						bet_3dd = 0;
						flag = false;
					}
					if (isNaN(nomor3dd)) {
						nomor3dd = "";
						flag = false;
					}
					if (isNaN(bet_3dd)) {
						bet_3dd = 0;
						flag = false;
					}
					if (flag) {
						form3dd_add();
					}
				}
				break;
			case "2DD":
				if (nomor2dd == "" && parseInt(bet_2dd) < minimal_bet) {
					nomor2dd_input.focus();
				} else {
					if (nomor2dd.length < 2){
						nomor2dd = "";
						bet_2dd = 0;
						flag = false;
					}
					if (isNaN(nomor2dd)) {
						nomor2dd = "";
						flag = false;
					}
					if (isNaN(bet_2dd)) {
						bet_2dd = 0;
						flag = false;
					}
					if (flag) {
						form2dd_add();
					}
				}
				break;
			case "2DT":
				if (nomor2dt == "" && parseInt(bet_2dt) < minimal_bet) {
					nomor2dt_input.focus();
				} else {
					if (nomor2dt.length < 2){
						nomor2dt = "";
						bet_2dt = 0;
						flag = false;
					}
					if (isNaN(nomor2dt)) {
						nomor2dt = "";
						flag = false;
					}
					if (isNaN(bet_2dt)) {
						bet_2dt = 0;
						flag = false;
					}
					if (flag) {
						form2dt_add();
					}
				}
				break;
			case "quick2D":
				if (quick_bet == "" && parseInt(quick_bet) < minimal_bet) {
					quick_bet_input.focus();
				} else {
					if (isNaN(quick_bet)) {
						quick_bet = 0;
						flag = false;
					}
					if (flag) {
						formquick2d_add();
					}
				}
				break;
			case "pilihan":
				path_432 = path
				idmodal = "modalpilihan432"
				myModal = new bootstrap.Modal(document.getElementById(idmodal));
				myModal.show();
				break;

		}
	};
	const handlePilihan = (e) => {
		flag_fulldiskon = e
		switch (path_432) {
			case "4-3-2":
				handleTambah('4-3-2')
				break;
			case "432SET":
				handleTambah('432SET');
				break;
			case "BBFS":
				handleTambah('BBFS');
				break;
			case "wap":
				handleTambah('wap');
				break;
			case "polatarung":
				handleTambah('polatarung');
				break;
			case "3DD":
				handleTambah('3DD');
				break;
			case "2DD":
				handleTambah('2DD');
				break;
			case "2DT":
				handleTambah('2DT');
				break;
			case "quick2D":
				handleTambah('quick2D');
				break;

		}
		myModal.hide();
	};
	const handleKeyboard_format = (e) => {
		let numbera;
		for (let i = 0; i < nomor_432.length; i++) {
			numbera = parseInt(nomor_432[i]);
			if (isNaN(numbera)) {
				if (nomor_432[i] != "*") {
					nomor_432 = "";
				}
			}
		}
		for (let i = 0; i < nomor3dd.length; i++) {
			numbera = parseInt(nomor3dd[i]);
			if (isNaN(numbera)) {
				nomor3dd = "";
			}
		}
		for (let i = 0; i < nomor2dd.length; i++) {
			numbera = parseInt(nomor2dd[i]);
			if (isNaN(numbera)) {
				nomor2dd = "";
			}
		}
		for (let i = 0; i < nomor2dt.length; i++) {
			numbera = parseInt(nomor2dt[i]);
			if (isNaN(numbera)) {
				nomor2dt = "";
			}
		}
		for (let i = 0; i < nomorbbfs.length; i++) {
			numbera = parseInt(nomorbbfs[i]);
			if (isNaN(nomorbbfs)) {
				nomorbbfs = "";
			}
		}
		for (let i = 0; i < nomorset.length; i++) {
			numbera = parseInt(nomorset[i]);
			if (isNaN(nomorset)) {
				nomorset = "";
			}
		}
	};
	const handleKeyboard_number = (e) => {
		let numbera;
		for (let i = 0; i < bet_432.length; i++) {
			numbera = parseInt(bet_432[i]);
			if (isNaN(numbera)) {
				bet_432 = "";
			}
		}
		for (let i = 0; i < bet_3dd.length; i++) {
			numbera = parseInt(bet_3dd[i]);
			if (isNaN(numbera)) {
				bet_3dd = "";
			}
		}
		for (let i = 0; i < betset_1.length; i++) {
			numbera = parseInt(betset_1[i]);
			if (isNaN(numbera)) {
				betset_1 = "";
			}
		}
		for (let i = 0; i < betset_2.length; i++) {
			numbera = parseInt(betset_2[i]);
			if (isNaN(numbera)) {
				betset_2 = "";
			}
		}
		for (let i = 0; i < betset_3.length; i++) {
			numbera = parseInt(betset_3[i]);
			if (isNaN(numbera)) {
				betset_3 = "";
			}
		}
		for (let i = 0; i < betset_4.length; i++) {
			numbera = parseInt(betset_4[i]);
			if (isNaN(numbera)) {
				betset_4 = "";
			}
		}
		for (let i = 0; i < betset_5.length; i++) {
			numbera = parseInt(betset_5[i]);
			if (isNaN(numbera)) {
				betset_5 = "";
			}
		}
		for (let i = 0; i < betset_6.length; i++) {
			numbera = parseInt(betset_6[i]);
			if (isNaN(numbera)) {
				betset_6 = "";
			}
		}
		for (let i = 0; i < bet_1.length; i++) {
			numbera = parseInt(bet_1[i]);
			if (isNaN(numbera)) {
				bet_1 = "";
			}
		}
		for (let i = 0; i < bet_2.length; i++) {
			numbera = parseInt(bet_2[i]);
			if (isNaN(numbera)) {
				bet_2 = "";
			}
		}
		for (let i = 0; i < bet_3.length; i++) {
			numbera = parseInt(bet_3[i]);
			if (isNaN(numbera)) {
				bet_3 = "";
			}
		}
		for (let i = 0; i < bet_4.length; i++) {
			numbera = parseInt(bet_4[i]);
			if (isNaN(numbera)) {
				bet_4 = "";
			}
		}
		for (let i = 0; i < bet_5.length; i++) {
			numbera = parseInt(bet_5[i]);
			if (isNaN(numbera)) {
				bet_5 = "";
			}
		}
		for (let i = 0; i < bet_2dd.length; i++) {
			numbera = parseInt(bet_2dd[i]);
			if (isNaN(numbera)) {
				bet_2dd = "";
			}
		}
		for (let i = 0; i < bet_2dt.length; i++) {
			numbera = parseInt(bet_2dt[i]);
			if (isNaN(numbera)) {
				bet_2dt = "";
			}
		}
		for (let i = 0; i < nomorbbfs.length; i++) {
			numbera = parseInt(nomorbbfs[i]);
			if (isNaN(numbera)) {
				nomorbbfs = "";
			}
		}
		for (let i = 0; i < nomor2dd.length; i++) {
			numbera = parseInt(nomor2dd[i]);
			if (isNaN(numbera)) {
				nomor2dd = "";
			}
		}
		for (let i = 0; i < nomor2dt.length; i++) {
			numbera = parseInt(nomor2dt[i]);
			if (isNaN(numbera)) {
				nomor2dt = "";
			}
		}
		for (let i = 0; i < quick_bet.length; i++) {
			numbera = parseInt(quick_bet[i]);
			if (isNaN(numbera)) {
				quick_bet = "";
			}
		}
		for (let i = 0; i < nomoras.length; i++) {
			numbera = parseInt(nomoras[i]);
			if (isNaN(nomoras)) {
				nomoras = "";
			}
		}
		for (let i = 0; i < nomorkop.length; i++) {
			numbera = parseInt(nomorkop[i]);
			if (isNaN(nomorkop)) {
				nomorkop = "";
			}
		}
		for (let i = 0; i < nomorkepala.length; i++) {
			numbera = parseInt(nomorkepala[i]);
			if (isNaN(nomorkepala)) {
				nomorkepala = "";
			}
		}
		for (let i = 0; i < nomorekor.length; i++) {
			numbera = parseInt(nomorekor[i]);
			if (isNaN(nomorekor)) {
				nomorekor = "";
			}
		}
		for (let i = 0; i < bet_tarung.length; i++) {
			numbera = parseInt(bet_tarung[i]);
			if (isNaN(bet_tarung)) {
				bet_tarung = "";
			}
		}
	};
	const handleKeyboard_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			handleTambah("pilihan","4-3-2")
		}
	};
	const handleKeyboard432set_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			handleTambah("pilihan","432SET")
		}
	};
	const handleKeyboardbbfs_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			handleTambah("pilihan","BBFS")
		}
	};
	const handleKeyboard3dd_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			handleTambah("pilihan","3DD")
		}
	};
	const handleKeyboard2dd_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			handleTambah("pilihan","2DD")
		}
	};
	const handleKeyboard2dt_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			handleTambah("pilihan","2DT")
		}
	};
	const handleKeyboardquick2d_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			handleTambah("pilihan","quick2D")
		}
	};
	const handleKeyboardpolatarung_checkenter = (e) => {
		let keyCode = e.which || e.keyCode;
		if (keyCode === 13) {
			handleTambah("pilihan","polatarung")
		}
	};
</script>

<Loader cssstyle={css_loader} />

{#if client_device == "WEBSITE"}
	<Card color="dark" style="border:1px solid #262424;margin:0px;padding:0px;">
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
					id="pills-form432d-tab"
					data-bs-toggle="pill"
					data-bs-target="#pills-form432d"
					type="button"
					role="tab"
					aria-controls="pills-form432d"
					aria-selected="true">4D/3D/2D</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-form432dset-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-form432dset"
					  type="button"
					  role="tab"
					  aria-controls="pills-form432dset"
					  aria-selected="true">4D/3D/2D SET</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-bolakbalik-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-bolakbalik"
					  type="button"
					  role="tab"
					  aria-controls="pills-bolakbalik"
					  aria-selected="true">BOLAK BALIK</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-wap-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-wap"
					  type="button"
					  role="tab"
					  aria-controls="pills-wap"
					  aria-selected="true">WAP</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-polatarung-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-polatarung"
					  type="button"
					  role="tab"
					  aria-controls="pills-polatarung"
					  aria-selected="true">POLA TARUNG</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-quick2d-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-quick2d"
					  type="button"
					  role="tab"
					  aria-controls="pills-quick2d"
					  aria-selected="true">QUICK 2D</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-3dd-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-3dd"
					  type="button"
					  role="tab"
					  aria-controls="pills-3dd"
					  aria-selected="true">3DD</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-2dd-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-2dd"
					  type="button"
					  role="tab"
					  aria-controls="pills-2dd"
					  aria-selected="true">2DD</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-2dt-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-2dt"
					  type="button"
					  role="tab"
					  aria-controls="pills-2dt"
					  aria-selected="true">2D TENGAH</button>
				</li>
			</ul>
			<div class="tab-content" id="nav-tabContent">
				<div class="tab-pane fade show active"
					id="pills-form432d"
					role="tabpanel"
					aria-labelledby="pills-form432d-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (2-4)</span>
									<input
										autofocus
										bind:this={nomor_432_input}
										bind:value={nomor_432}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 4D/3D/2D Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="4"
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
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_432}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span style="text-align:right;font-size:12px;color:#8a8a8a;">
										{new Intl.NumberFormat().format(bet_432)}
									</span>
								</td>
								<td
									width="20%"
									NOWRAP
									style="vertical-align: center;">
									<Button
										id="btn2"
										on:click={() => {
											handleTambah("pilihan","4-3-2");
										}}>TAMBAH</Button>
								</td>
							</tr>
						</table>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-form432dset"
					role="tabpanel"
					aria-labelledby="pills-form432dset-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;">
									<span style="color:#8a8a8a;">Nomor (2-4)</span>
									<input
										bind:this={nomorset_input}
										bind:value={nomorset}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 4D/3D/2D Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="4"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">4D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_1}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
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
											betset_1
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_3}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="2"/>
									<span style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
											betset_3
										)}</span>
									<br>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">3D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_2}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="1"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											betset_2
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2DD - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_4}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="3"/>
									<span style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
											betset_4
										)}</span>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">3DD - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_6}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="1"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											betset_6
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2DT - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_5}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="4"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											betset_5
										)}</span>
								</td>
							</tr>
							<tr>
								<td colspan="4">
									<div class="d-grid gap-1 mt-3">
										<Button
											id="btn2"
											on:click={() => {
												handleTambah("pilihan","432SET");
											}}>TAMBAH</Button>
									</div>
								</td>
							</tr>
						</table>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-bolakbalik"
					role="tabpanel"
					aria-labelledby="pills-bolakbalik-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;">
									<span style="color:#8a8a8a;">Nomor (2-{bbfs})</span>
									<input
										bind:this={nomorbbfs_input}
										bind:value={nomorbbfs}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 4D/3D/2D Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength={bbfs}
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">4D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_1}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
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
											bet_1
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_3}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="2"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_3
										)}</span>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">3D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_2}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="1"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_2
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2DD - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_4}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="3"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_4
										)}</span>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">3DD - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_6}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="1"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_6
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2DT - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_5}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="4"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;"
										>{new Intl.NumberFormat().format(
											bet_5
										)}</span>
								</td>
							</tr>
							<tr>
								<td colspan="4">
									<div class="d-grid gap-1 mt-3">
										<Button
											id="btn2"
											on:click={() => {
												handleTambah("pilihan","BBFS");
											}}>TAMBAH</Button>
									</div>
								</td>
							</tr>
						</table>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-wap"
					role="tabpanel"
					aria-labelledby="pills-wap-tab">
					<div style="margin:5px;">
						<textarea
							bind:this={nomorwap_input}
							bind:value={nomorwap}
							placeholder="Input Format"
							rows="100" cols="100"
							maxlength=1000 
							style="border:none;background:#303030;color:white;height:95px;resize:none;"
							class="form-control"/>
						<div class="d-grid gap-1 mt-3">
							<Button
								id="btn2"
								on:click={() => {
									handleTambah("pilihan","wap");
								}}>TAMBAH</Button>
						</div>
						<p class="p-3" style="font-size:12px;color:#8a8a8a;">
							<b>Contoh (WAP) :</b><br />
							1234*234*34#1000,34*235*35#5000<br />
						</p>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-polatarung"
					role="tabpanel"
					aria-labelledby="pills-polatarung-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor AS</span>
									<input
										bind:this={nomoras_input}
										bind:value={nomoras}
										on:keyup={handleKeyboard_number}
										type="text"
										class="form-control form-control-sm"
										placeholder="AS"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="4"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor KOP</span>
									<input
										bind:this={nomorkop_input}
										bind:value={nomorkop}
										on:keyup={handleKeyboard_number}
										type="text"
										class="form-control form-control-sm"
										placeholder="KOP"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="4"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor KEPALA</span>
									<input
										bind:value={nomorkepala}
										on:keyup={handleKeyboard_number}
										type="text"
										class="form-control form-control-sm"
										placeholder="KEPALA"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="4"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor EKOR</span>
									<input
										bind:value={nomorekor}
										on:keyup={handleKeyboard_number}
										type="text"
										class="form-control form-control-sm"
										placeholder="EKOR"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="4"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:this={bet_tarung_input}
										bind:value={bet_tarung}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardpolatarung_checkenter}
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
											bet_tarung
										)}</span>
								</td>
								<td
									width="20%"
									NOWRAP
									style="vertical-align: center;">
									<Button
										id="btn2"
										on:click={() => {
											handleTambah("pilihan","polatarung");
										}}>TAMBAH</Button>
								</td>
							</tr>
						</table>
						<p class="p-3" style="font-size:12px;color:#8a8a8a;">
							POLA TARUNG : AS KOP KEPALA EKOR <br>
							<b>Contoh (POLA TARUNG) :</b><br />
							- 123 456 789 012 => 4D<br>
							- 12 45 78 => 3D<br>
							- 12 45  => 2D<br>
						</p>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-quick2d"
					role="tabpanel"
					aria-labelledby="pills-quick2d-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Besar/Kecil/Genap/Ganjil</span>
									<select
										bind:value={quick_pilihan1}
										bind:this={quick_pilihan1_input}
										style="border:none;background:#303030;color:white;"
										class="form-control">
										<option value="BESAR">BESAR</option>
										<option value="KECIL">KECIL</option>
										<option value="GENAP">GENAP</option>
										<option value="GANJIL">GANJIL</option>
									</select>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="15%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Besar/Kecil/Genap/Ganjil</span>
									<select
										bind:value={quick_pilihan2}
										bind:this={quick_pilihan2_input}
										style="border:none;background:#303030;color:white;"
										class="form-control">
										<option value="2D">2D</option>
										<option value="2DD">2D DEPAN</option>
										<option value="2DT">2D TENGAH</option>
									</select>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={quick_bet}
										bind:this={quick_bet_input}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardquick2d_checkenter}
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
											quick_bet
										)}</span>
								</td>
								<td
									width="20%"
									NOWRAP
									style="vertical-align: center;">
									<Button
										id="btn2"
										on:click={() => {
											handleTambah("pilihan","quick2D");
										}}>TAMBAH</Button>
								</td>
							</tr>
						</table>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-3dd"
					role="tabpanel"
					aria-labelledby="pills-3dd-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (3 digit)</span>
									<input
										bind:this={nomor3dd_input}
										bind:value={nomor3dd}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard3dd_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 3DD Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="3"
										maxlength="3"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_3dd}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard3dd_checkenter}
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
											bet_3dd
										)}</span>
								</td>
								<td
									width="20%"
									NOWRAP
									style="vertical-align: center;">
									<Button
										id="btn2"
										on:click={() => {
											handleTambah("pilihan","3DD");
										}}>TAMBAH</Button>
								</td>
							</tr>
						</table>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-2dd"
					role="tabpanel"
					aria-labelledby="pills-2dd-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (2 digit)</span>
									<input
										bind:this={nomor2dd_input}
										bind:value={nomor2dd}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard2dd_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 2DD Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="2"
										maxlength="2"
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
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_2dd}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard2dd_checkenter}
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
											bet_2dd
										)}</span>
								</td>
								<td
									width="20%"
									NOWRAP
									style="vertical-align: center;">
									<Button
										id="btn2"
										on:click={() => {
											handleTambah("pilihan","2DD");
										}}>TAMBAH</Button>
								</td>
							</tr>
						</table>
					</div>
				</div>
				<div class="tab-pane fade "
					id="pills-2dt"
					role="tabpanel"
					aria-labelledby="pills-2dt-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (2 digit)</span>
									<input
										bind:this={nomor2dt_input}
										bind:value={nomor2dt}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard2dt_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 2DT Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="2"
										maxlength="2"
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
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_2dt}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard2dt_checkenter}
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
											bet_2dt
										)}</span>
								</td>
								<td
									width="20%"
									NOWRAP
									style="vertical-align: center;">
									<Button
										id="btn2"
										on:click={() => {
											handleTambah("pilihan","2DT");
										}}>TAMBAH</Button>
								</td>
							</tr>
						</table>
					</div>
				</div>
			</div>		
		</CardBody>
	</Card>
{:else}
	<Card color="dark" style="border:1px solid #262424;margin:0px;padding:0px;">
		<CardHeader style="background:#323030;border-bottom:1px solid #333;border-top: 0 solid #333;">
			<div class="float-end">
				<div style="color:white;text-align:right;font-size:12px;font-weight:bold;">
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
					id="pills-form432d-tab"
					data-bs-toggle="pill"
					data-bs-target="#pills-form432d"
					type="button"
					role="tab"
					aria-controls="pills-form432d"
					aria-selected="true">4D/3D/2D</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-form432dset-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-form432dset"
					  type="button"
					  role="tab"
					  aria-controls="pills-form432dset"
					  aria-selected="true">SET</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-bolakbalik-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-bolakbalik"
					  type="button"
					  role="tab"
					  aria-controls="pills-bolakbalik"
					  aria-selected="true">BB</button>
				</li>
				<li class="nav-item">
					<button
					  class="nav-link"
					  id="pills-wap-tab"
					  data-bs-toggle="pill"
					  data-bs-target="#pills-wap"
					  type="button"
					  role="tab"
					  aria-controls="pills-wap"
					  aria-selected="true">WAP</button>
				</li>
				<li class="nav-item">
					<a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button" aria-expanded="false">OTHERS</a>
					<ul class="dropdown-menu">
						<li>
							<button
								class="dropdown-item"
								id="pills-3dd-tab"
								data-bs-toggle="pill"
								data-bs-target="#pills-3dd"
								type="button"
								role="tab"
								aria-controls="pills-3dd"
								aria-selected="true">3DD</button>
						</li>
						<li>
							<button
								class="dropdown-item"
								id="pills-2dd-tab"
								data-bs-toggle="pill"
								data-bs-target="#pills-2dd"
								type="button"
								role="tab"
								aria-controls="pills-2dd"
								aria-selected="true">2DD</button>
						</li>
						<li>
							<button
								class="dropdown-item"
								id="pills-2dt-tab"
								data-bs-toggle="pill"
								data-bs-target="#pills-2dt"
								type="button"
								role="tab"
								aria-controls="pills-2dt"
								aria-selected="true">2D TENGAH</button>
						</li>
					</ul>
				</li>
			</ul>
			<div class="tab-content" id="nav-tabContent">
				<div class="tab-pane fade show active"
					id="pills-form432d"
					role="tabpanel"
					aria-labelledby="pills-form432d-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="35%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (2-4)</span>
									<input
										bind:this={nomor_432_input}
										bind:value={nomor_432}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 4D/3D/2D Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="4"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_432}
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
											bet_432
										)}</span>
								</td>
							</tr>
							<tr>
								<td
									colspan="2"
									NOWRAP
									style="vertical-align: center;"/>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("pilihan","4-3-2");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade"
					id="pills-form432dset"
					role="tabpanel"
					aria-labelledby="pills-form432dset-tab">
					<div class="table-responsive" style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									colspan="3"
									NOWRAP
									style="padding-right:10px;vertical-align: top;">
									<span style="color:#8a8a8a;">Nomor (2-4)</span>
									<input
										bind:this={nomorset_input}
										bind:value={nomorset}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 4D/3D/2D Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength="4"
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
							</tr>
							<tr>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">4D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_1}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
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
											betset_1
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_3}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
											betset_3
										)}</span>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">3D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_2}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
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
											betset_2
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2DD - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_4}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
											betset_4
										)}</span>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">3DD - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_6}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
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
											betset_6
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2DT - Bet (min : {minimal_bet})</span>
									<input
										bind:value={betset_5}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard432set_checkenter}
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
											betset_5
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("pilihan","432SET");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade"
					id="pills-bolakbalik"
					role="tabpanel"
					aria-labelledby="pills-bolakbalik-tab">
					<div class="table-responsive" style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									colspan="3"
									NOWRAP
									style="padding-right:10px;vertical-align: top;">
									<span style="color:#8a8a8a;">Nomor (2-{bbfs})</span>
									<input
										bind:this={nomorbbfs_input}
										bind:value={nomorbbfs}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 4D/3D/2D Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="4"
										maxlength={bbfs}
										tab_index="-1"
										autocomplete="off"/>
									<span
										class="help-block"
										style="text-align:right;font-size:12px;"/>
								</td>
							</tr>
							<tr>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">4D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_1}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
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
											bet_1
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_3}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
											bet_3
										)}</span>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">3D - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_2}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
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
											bet_2
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2DD - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_4}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
										type="text"
										class="form-control"
										placeholder="Bet"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:right;"
										minlength="3"
										maxlength="7"
										tab_index="0"/>
									<span
										style="text-align:right;font-size:12px;color:#8a8a8a;">{new Intl.NumberFormat().format(
											bet_4
										)}</span>
								</td>
								<td
									width="22%"
									NOWRAP
									style="padding-right:10px;vertical-align: top;text-align:right;">
									<span style="color:#8a8a8a;">3DD - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_6}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
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
											bet_6
										)}</span>
									<br>
									<span style="color:#8a8a8a;">2DT - Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_5}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboardbbfs_checkenter}
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
											bet_5
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("pilihan","BBFS");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade"
					id="pills-wap"
					role="tabpanel"
					aria-labelledby="pills-wap-tab">
					<div class="d-grid gap-1">
						<textarea
							bind:this={nomorwap_input}
							bind:value={nomorwap}
							placeholder="Input Format"
							rows="100" cols="100"
							maxlength=1000 
							style="border:none;background:#303030;color:white;height:95px;resize:none;"
							class="form-control"
						/>
						<Button
							id="btn2"
							on:click={() => {
								handleTambah("wap");
							}}>TAMBAH</Button
						>
						<p style="font-size:12px;color:#8a8a8a;">
							<b>Contoh (WAP) :</b><br />
							1234*234*34#1000,34*235*35#5000<br />
						</p>
					</div>
				</div>
				<div class="tab-pane fade"
					id="pills-3dd"
					role="tabpanel"
					aria-labelledby="pills-3dd-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (3 digit)</span>
									<input
										bind:this={nomor3dd_input}
										bind:value={nomor3dd}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard3dd_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 3DD Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="3"
										maxlength="3"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_3dd}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard2dd_checkenter}
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
											bet_3dd
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("3DD");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade"
					id="pills-2dd"
					role="tabpanel"
					aria-labelledby="pills-2dd-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (2 digit)</span>
									<input
										bind:this={nomor2dd_input}
										bind:value={nomor2dd}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard2dd_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 2DD Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="2"
										maxlength="2"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_2dd}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard2dd_checkenter}
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
											bet_2dd
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("pilihan","2DD");
							}}>TAMBAH</Button>
					</div>
				</div>
				<div class="tab-pane fade"
					id="pills-2dt"
					role="tabpanel"
					aria-labelledby="pills-2dt-tab">
					<div style="margin:5px;">
						<table
							class="table"
							style="background:none;width:100%;">
							<tr>
								<td
									width="25%"
									NOWRAP
									style="padding-right:10px;vertical-align: center;">
									<span style="color:#8a8a8a;">Nomor (2 digit)</span>
									<input
										bind:this={nomor2dt_input}
										bind:value={nomor2dt}
										on:keyup={handleKeyboard_format}
										on:keypress={handleKeyboard2dt_checkenter}
										type="text"
										class="form-control form-control-sm"
										placeholder="Input 2DT Digit"
										style="border:none;background:#303030;color:white;font-size:20px;text-align:center;"
										minlength="2"
										maxlength="2"
										tab_index="-1"
										autocomplete="off"/>
									<span class="help-block" style="text-align:right;font-size:12px;"/>
								</td>
								<td
									width="*"
									NOWRAP
									style="padding-right:10px;vertical-align: center;text-align:right;">
									<span style="color:#8a8a8a;">Bet (min : {minimal_bet})</span>
									<input
										bind:value={bet_2dt}
										on:keyup={handleKeyboard_number}
										on:keypress={handleKeyboard2dt_checkenter}
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
											bet_2dt
										)}</span>
								</td>
							</tr>
						</table>
						<Button
							block
							id="btn2"
							on:click={() => {
								handleTambah("pilihan","2DT");
							}}>TAMBAH</Button>
					</div>
				</div>
			</div>
		</CardBody>
	</Card>
{/if}

<Modal2
    modal_id={"modalpilihan432"}
    modal_footer_flag={false}
    modal_size={"modal-dialog-centered"}>
    <slot:template slot="body">
       <center style="margin-top:20px;margin-bottom:20px;">
		<span style="color: white;font-weight:12px;">Pilih Permainan dibawah ini : </span>
		<br />
		<button
			on:click={() => {
				handlePilihan("DISC");
			}} 
			class="btn btn-info btn-lg">DISKON</button>
		<button
			on:click={() => {
				handlePilihan("FULL");
			}} 
			class="btn btn-info btn-lg">NON DISKON / FULL</button>
		<button
			on:click={() => {
				handlePilihan("BB");
			}} 
			class="btn btn-info btn-lg">BOLAK BALIK / BB</button>
	   </center>
    </slot:template>
</Modal2>

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
<Tablekeranjang
	on:removekeranjang={removekeranjang}
	on:removekeranjangall={removekeranjangall}
	on:handleSave={handleSave}
	{client_device}
	{group_btn_beli}
	{count_line_4d}
	{count_line_3d}
	{count_line_3dd}
	{count_line_2d}
	{count_line_2dd}
	{count_line_2dt}
	{keranjang}
	{totalkeranjang}
	{minimal_bet}
	{max4d_bet}
	{max3d_bet}
	{max3dd_bet}
	{max2d_bet}
	{max2dd_bet}
	{max2dt_bet}
	{disc4d_bet}
	{disc3d_bet}
	{disc3dd_bet}
	{disc2d_bet}
	{disc2dd_bet}
	{disc2dt_bet}
	{win4d_bet}
	{win3d_bet}
	{win3dd_bet}
	{win2d_bet}
	{win2dd_bet}
	{win2dt_bet}
	{win4dnodiskon_bet}
	{win3dnodiskon_bet}
	{win3ddnodiskon_bet}
	{win2dnodiskon_bet}
	{win2ddnodiskon_bet}
	{win2dtnodiskon_bet}
	{win4dbb_kena_bet}
	{win3dbb_kena_bet}
	{win3ddbb_kena_bet}
	{win2dbb_kena_bet}
	{win2ddbb_kena_bet}
	{win2dtbb_kena_bet}
	{win4dbb_bet}
	{win3dbb_bet}
	{win3ddbb_bet}
	{win2dbb_bet}
	{win2ddbb_bet}
	{win2dtbb_bet}
	{limitline_4d}
	{limitline_3d}
	{limitline_3dd}
	{limitline_2d}
	{limitline_2dd}
	{limitline_2dt}
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
