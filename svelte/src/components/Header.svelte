<script>
    import { Col, Card, CardBody } from "sveltestrap";
    import dayjs from "dayjs";
    import utc from "dayjs/plugin/utc";
    import timezone from "dayjs/plugin/timezone";
    import Modal from "../components/Modalfull2.svelte";
    import Placeholder from "../components/Placeholder.svelte";
    dayjs.extend(utc);
    dayjs.extend(timezone);

    export let client_token = "";
    export let client_company = "";
    export let client_username = "";
    export let client_credit = 0;
    export let client_ipaddress = "";
    export let client_timezone = "";
    export let client_device = "";

    let modal_table_fontsize_header = "13px";
    let modal_table_fontsize_body = "12px";
    let modal_table_fontsize_bukumimpi_header = "13px";
    if (client_device == "MOBILE") {
        modal_table_fontsize_bukumimpi_header = "12px";
        modal_table_fontsize_header = "11px";
        modal_table_fontsize_body = "11px";
    }
    let display_credit = 0;
    let clockmachine = "";
    let record = "";
    let filterBukuMimpi = [];
    let listBukumimpi = [];
    let listhasilkeluaran = [];
    let resulttogel = [];
    let listhasilinvoice = [];
    let listhasilinvoicebet = [];
    let searchbukumimpi = "";
    let tipe = "";
    let idinvoiceall = "";
    let detailslipheader = "";
    let detailslipheaderpermainan = "";
    let nmpasaran = "";
    let total4d_bayar = 0;
    let total3d_bayar = 0;
    let total2d_bayar = 0;
    let totalcolokbebas_bayar = 0;
    let totalcolokmacau_bayar = 0;
    let totalcoloknaga_bayar = 0;
    let totalcolokjitu_bayar = 0;
    let total5050umum_bayar = 0;
    let total5050special_bayar = 0;
    let total5050kombinasi_bayar = 0;
    let totalmacaukombinasi_bayar = 0;
    let totaldasar_bayar = 0;
    let totalshio_bayar = 0;
    let totalwin_4d = 0;
    let totalwin_3d = 0;
    let totalwin_2d = 0;
    let totalwin_colokbebas = 0;
    let totalwin_colokmacau = 0;
    let totalwin_coloknaga = 0;
    let totalwin_colokjitu = 0;
    let totalwin_5050umum = 0;
    let totalwin_5050special = 0;
    let totalwin_5050kombinasi = 0;
    let totalwin_macaukombinasi = 0;
    let totalwin_dasar = 0;
    let totalwin_shio = 0;
    let subtotal_bayar = 0;
    let subtotal_winner = 0;
    let total_winlose = 0;
    function updateClock() {
        let endtime = dayjs()
            .tz(client_timezone)
            .format("DD MMM YYYY | HH:mm:ss");

        clockmachine = endtime;
    }
    async function fetch_bukumimpi() {
        const res = await fetch("/api/bookdream", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                tipe: tipe,
                nama: searchbukumimpi.toLowerCase(),
            }),
        });

        const json = await res.json();
        if (json.status == 200) {
            record = json.record;
            if (record != null) {
                for (var i = 0; i < record.length; i++) {
                    listBukumimpi = [
                        ...listBukumimpi,
                        {
                            bukumimpi_tipe: record[i]["bukumimpi_tipe"],
                            bukumimpi_nama: record[i]["bukumimpi_nama"],
                            bukumimpi_nomor: record[i]["bukumimpi_nomor"],
                        },
                    ];
                }
            } else {
                alert("Error");
            }
        } else {
            alert("Error");
        }
    }
    async function fetch_resultall() {
        listhasilkeluaran = [];
        const res = await fetch("/api/resulttogelall", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                company: client_company,
            }),
        });

        const json = await res.json();
        if (json.status == 200) {
            record = json.record;
            if (record != null) {
                for (var i = 0; i < record.length; i++) {
                    listhasilkeluaran = [
                        ...listhasilkeluaran,
                        {
                            keluaran_no: record[i]["no"],
                            keluaran_date: dayjs(record[i]["date"])
                                .tz(client_timezone)
                                .format("DD MMM YYYY"),
                            keluaran_pasaran: record[i]["pasaran"],
                            keluaran_pasarancode: record[i]["pasaran_code"],
                            keluaran_periode: record[i]["periode"],
                            keluaran_result: record[i]["result"],
                        },
                    ];
                }
                console.log(listhasilkeluaran);
            } else {
                alert("Error");
            }
        } else {
            alert("Error");
        }
    }
    async function fetch_resultbypasaran(e, y) {
        nmpasaran = y;
        const res = await fetch("/api/resulttogel", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                company: client_company,
                pasaran_code: e,
            }),
        });

        const json = await res.json();
        record = json.record;
        if (json.status == 200) {
            record = json.record;
            if (record != null) {
                for (var i = 0; i < record.length; i++) {
                    resulttogel = [
                        ...resulttogel,
                        {
                            no: record[i]["no"],
                            date: dayjs(record[i]["date"]).format(
                                "DD MMM YYYY"
                            ),
                            periode: record[i]["periode"],
                            result: record[i]["result"],
                        },
                    ];
                }
                let myModal = new bootstrap.Modal(
                    document.getElementById("modalhasilkeluaranpasaran")
                );
                myModal.show();
            }
        }
    }
    async function fetch_invoicell() {
        listhasilinvoice = [];
        const res = await fetch("/api/slipperiodeall", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                company: client_company,
                username: client_username,
            }),
        });

        const json = await res.json();
        if (json.status == 200) {
            record = json.record;
            if (record != null) {
                for (var i = 0; i < record.length; i++) {
                    listhasilinvoice = [
                        ...listhasilinvoice,
                        {
                            invoice_idinvoice: record[i]["idinvoice"],
                            invoice_tglkeluaran: dayjs(record[i]["tglkeluaran"])
                                .tz(client_timezone)
                                .format("DD MMM YYYY"),
                            invoice_pasaran: record[i]["pasaran"],
                            invoice_periode: record[i]["periode"],
                            invoice_status: record[i]["status"],
                            invoice_totalbet: record[i]["totalbet"],
                            invoice_totalbayar: record[i]["totalbayar"],
                            invoice_totalwin: record[i]["totalwin"],
                            invoice_totallose: record[i]["totallose"],
                            invoice_background: record[i]["background"],
                            invoice_color_lost: record[i]["color_lost"],
                            invoice_color_totalloset:
                                record[i]["color_totallose"],
                        },
                    ];
                }
            } else {
                alert("Error");
            }
        } else {
            alert("Error");
        }
    }
    async function fetch_invoicelldetail(e, periode) {
        detailslipheader = periode;
        idinvoiceall = e;
        const res = await fetch("/api/slipperiodedetail", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                company: client_company,
                username: client_username,
                idinvoice: e,
            }),
        });

        const json = await res.json();
        record = json.record;

        if (json.status == 200) {
            record = json.record;
            total4d_bayar = record["total4d_bayar"];
            total3d_bayar = record["total3d_bayar"];
            total2d_bayar = record["total2d_bayar"];
            totalcolokbebas_bayar = record["totalcolokbebas_bayar"];
            totalcolokmacau_bayar = record["totalcolokmacau_bayar"];
            totalcoloknaga_bayar = record["totalcoloknaga_bayar"];
            totalcolokjitu_bayar = record["totalcolokjitu_bayar"];
            total5050umum_bayar = record["total5050umum_bayar"];
            total5050special_bayar = record["total5050special_bayar"];
            total5050kombinasi_bayar = record["total5050kombinasi_bayar"];
            totalmacaukombinasi_bayar = record["totalmacaukombinasi_bayar"];
            totaldasar_bayar = record["totaldasar_bayar"];
            totalshio_bayar = record["totalshio_bayar"];
            totalwin_4d = record["totalwin_4d"];
            totalwin_3d = record["totalwin_3d"];
            totalwin_2d = record["totalwin_2d"];
            totalwin_colokbebas = record["totalwin_colokbebas"];
            totalwin_colokmacau = record["totalwin_colokmacau"];
            totalwin_coloknaga = record["totalwin_coloknaga"];
            totalwin_colokjitu = record["totalwin_colokjitu"];
            totalwin_5050umum = record["totalwin_5050umum"];
            totalwin_5050special = record["totalwin_5050special"];
            totalwin_5050kombinasi = record["totalwin_5050kombinasi"];
            totalwin_macaukombinasi = record["totalwin_macaukombinasi"];
            totalwin_dasar = record["totalwin_dasar"];
            totalwin_shio = record["totalwin_shio"];
            subtotal_bayar = record["subtotal_bayar"];
            subtotal_winner = record["subtotal_winner"];
            total_winlose = record["total_winlose"];
        }

        let myModal = new bootstrap.Modal(
            document.getElementById("modalslipalldetail")
        );
        myModal.show();
    }
    async function fetch_invoicealldetailpermainan(permainan, bayar) {
        if (parseInt(bayar) > 0) {
            detailslipheaderpermainan = permainan;
            listhasilinvoicebet = [];
            const res = await fetch("/api/invoicebetdetail", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    invoice: parseInt(idinvoiceall),
                    company: client_company,
                    username: client_username,
                    permainan: permainan,
                }),
            });

            const json = await res.json();
            if (json.status == 200) {
                record = json.record;
                if (record != null) {
                    for (var i = 0; i < record.length; i++) {
                        let status = record[i]["status"];
                        let background = "";
                        switch (status) {
                            case "RUNNING":
                                background =
                                    "background:#FFEB3B;font-weight:bold;color:black;";
                                break;
                            case "WINNER":
                                background =
                                    "background:#8BC34A;font-weight:bold;color:black;";
                                break;
                            case "LOSE":
                                background =
                                    "background:#E91E63;font-weight:bold;color:white;";
                                break;
                        }
                        listhasilinvoicebet = [
                            ...listhasilinvoicebet,
                            {
                                bet_no: record[i]["no"],
                                bet_background: background,
                                bet_status: record[i]["status"],
                                bet_tipe: record[i]["tipe"],
                                bet_permainan: record[i]["permainan"],
                                bet_nomor: record[i]["nomor"],
                                bet_bet: record[i]["bet"],
                                bet_diskon: record[i]["diskon"],
                                bet_kei: record[i]["kei"],
                                bet_bayar: record[i]["bayar"],
                                bet_win: record[i]["win"],
                            },
                        ];
                    }
                    let myModal = new bootstrap.Modal(
                        document.getElementById("modalslipalldetailbyid")
                    );
                    myModal.show();
                } else {
                    alert("Error");
                }
            } else {
                alert("Error");
            }
        } else {
            alert("Data Not Found");
        }
    }
    $: {
        setInterval(updateClock, 100);
        if (searchbukumimpi) {
            filterBukuMimpi = listBukumimpi.filter((item) =>
                item.bukumimpi_nama
                    .toLowerCase()
                    .includes(searchbukumimpi.toLowerCase())
            );
        } else {
            filterBukuMimpi = [...listBukumimpi];
        }
    }
    display_credit = new Intl.NumberFormat().format(client_credit);

    const handleClickButtonTop = (e) => {
        let idmodal = "";
        switch (e) {
            case "result":
                idmodal = "modalhasilkeluaran";
                fetch_resultall();
                break;
            case "invoice":
                idmodal = "modalhasilinvoice";
                fetch_invoicell();
                break;
            case "bukumimpi":
                idmodal = "modalbukumimpi";
                fetch_bukumimpi();
                break;
        }
        let myModal = new bootstrap.Modal(document.getElementById(idmodal));
        myModal.show();
    };
    const handleClickBukuMimpi = (e) => {
        filterBukuMimpi = [];
        listBukumimpi = [];
        switch (e) {
            case "ALL":
                tipe = "";
                searchbukumimpi = "";
                break;
            case "4D":
                tipe = "4D";
                searchbukumimpi = "";
                break;
            case "3D":
                tipe = "3D";
                searchbukumimpi = "";
                break;
            case "2D":
                tipe = "2D";
                searchbukumimpi = "";
                break;
        }
        fetch_bukumimpi();
    };
    const handleKeyboardbukumimpi_checkenter = (e) => {
        let keyCode = e.which || e.keyCode;
        if (keyCode === 13) {
            filterBukuMimpi = [];
            listBukumimpi = [];
            fetch_bukumimpi();
        }
    };
</script>

{#if client_device == "WEBSITE"}
    <nav class="navbar fixed-top " style="background-color: #252525;margin-bottom:100px;">
        <div class="container">
                <div class="col">
                    <a href="/?token={client_token}" title="totoapp">
                        <img
                            id="imglogo"
                            alt="SDSB4D"
                            style="margin-top:0px;"
                            src="logo.svg"/>
                    </a>
                </div>
                <div class="col">
                    <center>
                        <form class="d-flex">
                            <button
                                on:click={() => {
                                    handleClickButtonTop("result");
                                }}
                                id="btn1"
                                class="btn btn-secondary"
                                type="button">RESULT</button>
                            &nbsp;
                            <button
                                on:click={() => {
                                    handleClickButtonTop("invoice");
                                }}
                                id="btn1"
                                class="btn btn-secondary"
                                type="button">INVOICE</button>
                            &nbsp;
                            <button
                                on:click={() => {
                                    handleClickButtonTop("bukumimpi");
                                }}
                                id="btn1"
                                class="btn btn-secondary"
                                type="button">BUKU MIMPI</button>
                        </form>
                    </center>
                </div>
                <div class="col">
                    <Card color="dark" style="border:none;background-color:#252525;">
                        <CardBody style="background-color:#252525;text-align:right;">
                            <span style="font-size:12px;">TIMEZONE : <span id="style_text">{client_timezone}</span>  <span id="style_text">{clockmachine} WIB</span><br />
                            <span style="font-size:12px;">{client_username}</span>&nbsp;(<span id="style_text">{client_ipaddress}</span>)<br />
                            <span style="font-size:12px;">Credit : IDR <span id="style_text">{display_credit}</span><br />
                        </CardBody>
                    </Card>
                </div>
            
        </div>
    </nav>
    <div style="margin-top:100px;">&nbsp;</div>
{:else}
    <center style="margin-bottom:5px;">
        <a href="/?token={client_token}" title="SDSB4D">
            <img
                id="imglogo"
                alt="SDSB4D"
                style="margin-top:10px;"
                src="logo.svg"/>
        </a>
    </center>
    <Col
        xxl="12"
        xl="12"
        lg="12"
        md="12"
        sm="12"
        style="padding:5px;margin:0px;">
        <Card color="dark">
            <CardBody style="background-color:#2b3038;">
                <span style="font-size:12px;">Welcome, {client_username}</span
                ><br />
                <span style="font-size:12px;"
                    >Credit : IDR <span id="style_text">{display_credit}</span
                    ></span
                ><br />
                <span style="font-size:12px;"
                    >IPADDRESS : <span id="style_text">{client_ipaddress}</span
                    ></span
                ><br />
                <span style="font-size:12px;"
                    >TIMEZONE : <span id="style_text">{client_timezone}</span
                    ></span
                ><br />
                <span style="font-size:12px;"
                    >CLOCK : <span id="style_text">{clockmachine} WIB</span
                    ></span
                >
            </CardBody>
        </Card>
    </Col>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button
            on:click={() => {
                handleClickButtonTop("result");
            }}
            id="btn1"
            class="btn btn-secondary "
            type="button">RESULT</button
        >&nbsp;
        <button
            on:click={() => {
                handleClickButtonTop("invoice");
            }}
            id="btn1"
            class="btn btn-secondary"
            type="button">INVOICE</button
        >&nbsp;
        <button
            on:click={() => {
                handleClickButtonTop("bukumimpi");
            }}
            id="btn1"
            class="btn btn-secondary"
            type="button">BUKU MIMPI</button
        >
    </div>
{/if}

<div class="clearfix " />
<Modal
    modal_id={"modalhasilkeluaran"}
    modal_footer_flag={false}
    modal_body_height={"height:350px;"}
    modal_size={"modal-dialog-centered"}>
    <slot:template slot="header">
        <h5 class="modal-title">RESULT</h5>
    </slot:template>
    <slot:template slot="body">
        {#if listhasilkeluaran != ""}
        <table class="table table-dark table-striped">
            <thead>
                <tr>
                    <th
                        width="1%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:1px solid #303030;">NO</th>
                    <th
                        width="15%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">TANGGAL</th>
                    <th
                        width="*"
                        style="text-align:left;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">PASARAN</th>
                    <th
                        width="15%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">PERIODE</th>
                    <th
                        width="25%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">HASIL</th>
                </tr>
            </thead>
            <tbody>
                {#each listhasilkeluaran as rec}
                    <tr>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.keluaran_no}</td>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.keluaran_date}</td>
                        <td
                            on:click={() => {
                                fetch_resultbypasaran(
                                    rec.keluaran_pasarancode,
                                    rec.keluaran_pasaran
                                );
                            }}
                            NOWRAP
                            style="text-decoration:underline;cursor:pointer;text-align: left;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.keluaran_pasaran}</td>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.keluaran_periode}</td>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};color:rgb(255, 204, 0);">{rec.keluaran_result}</td>
                    </tr>
                {/each}
            </tbody>
        </table>
        {:else}
        <Placeholder total_placeholder="3" card_style="background-color:#2c2c2c;border:none;margin-top:5px;" />
        {/if}
    </slot:template>
</Modal>
<Modal
    modal_id={"modalhasilkeluaranpasaran"}
    modal_footer_flag={false}
    modal_body_height={"height:350px;"}
    modal_size={"modal-dialog-centered"}>
    <slot:template slot="header">
        <h5 class="modal-title">PASARAN : {nmpasaran}</h5>
    </slot:template>
    <slot:template slot="body">
        {#if resulttogel != ""}
        <table class="table table-dark table-striped">
            <thead>
                <tr>
                    <th
                        width="1%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">NO</th>
                    <th
                        width="15%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">TANGGAL</th>
                    <th
                        width="15%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">PERIODE</th>
                    <th
                        width="25%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">HASIL</th>
                </tr>
            </thead>
            <tbody>
                {#each resulttogel as rec}
                    <tr>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.no}</td>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.date}</td>

                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.periode}</td>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};color:rgb(255, 204, 0);">{rec.result}</td>
                    </tr>
                {/each}
            </tbody>
        </table>
        {:else}
        <Placeholder total_placeholder="3" card_style="background-color:#2c2c2c;border:none;margin-top:5px;" />
        {/if}
    </slot:template>
</Modal>
<Modal
    modal_id={"modalhasilinvoice"}
    modal_footer_flag={false}
    modal_body_height={"height:350px;"}
    modal_size={"modal-dialog-centered"}>
    <slot:template slot="header">
        <h5 class="modal-title">INVOICE</h5>
    </slot:template>
    <slot:template slot="body">
        {#if listhasilinvoice != ""}
        <table class="table table-dark">
            <thead>
                <tr>
                    <th
                        width="1%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">STATUS</th>
                    <th
                        width="15%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">TANGGAL</th>
                    <th
                        width="*"
                        style="text-align:left;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">PASARAN</th>
                    <th
                        width="15%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">PERIODE</th>
                    <th
                        width="25%"
                        style="text-align:right;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">WINLOSE</th>
                </tr>
            </thead>
            <tbody>
                {#each listhasilinvoice as rec}
                    <tr>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;;">
                            <span style="padding:5px;border-radius:5px;{rec.invoice_background}">{rec.invoice_status}</span> 
                        </td>
                        <td
                            NOWRAP
                            style="text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.invoice_tglkeluaran}</td>
                        <td
                            NOWRAP
                            style="text-align: left;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.invoice_pasaran}</td>
                        <td
                            on:click={() => {
                                fetch_invoicelldetail(
                                    rec.invoice_idinvoice,
                                    rec.invoice_periode
                                );
                            }}
                            NOWRAP
                            style="text-decoration:underline;cursor:pointer;text-align: center;vertical-align: top;font-size:{modal_table_fontsize_body};">{rec.invoice_periode}</td>
                        <td
                            NOWRAP
                            style="text-align: right;vertical-align: top;font-size:{modal_table_fontsize_body};color:#fc0;">{new Intl.NumberFormat().format(rec.invoice_totallose)}</td>
                    </tr>
                {/each}
            </tbody>
        </table>
        {:else}
            <Placeholder total_placeholder="5" card_style="background-color:#2c2c2c;border:none;margin-top:5px;" />
        {/if}
    </slot:template>
</Modal>
<Modal
    modal_id={"modalbukumimpi"}
    modal_headerbootom_flag={true}
    modal_footer_flag={false}
    modal_body_height={"height:500px;"}
    modal_size={"modal-dialog-centered"}>
    <slot:template slot="header">
        <h5 class="modal-title">BUKU MIMPI</h5>
    </slot:template>
    <slot:template slot="headerbottom">
        <ul
            class="nav nav-pills mb-3"
            id="pills-tab"
            role="tablist"
            style="background-color: #181818;">
            <li
                on:click={() => {
                    handleClickBukuMimpi("ALL");
                }}
                class="nav-item"
                role="presentation">
                <button
                    class="nav-link active"
                    id="pills-home-tab"
                    data-bs-toggle="pill"
                    data-bs-target="#pills-bukumimpiall"
                    type="button"
                    role="tab"
                    aria-controls="pills-bukumimpiall"
                    aria-selected="true">ALL</button>
            </li>
            <li
                on:click={() => {
                    handleClickBukuMimpi("4D");
                }}
                class="nav-item"
                role="presentation">
                <button
                    class="nav-link"
                    id="pills-profile-tab"
                    data-bs-toggle="pill"
                    data-bs-target="#pills-bukumimpi4d"
                    type="button"
                    role="tab"
                    aria-controls="pills-bukumimpi4d"
                    aria-selected="false">4D</button>
            </li>
            <li
                on:click={() => {
                    handleClickBukuMimpi("3D");
                }}
                class="nav-item"
                role="presentation">
                <button
                    class="nav-link"
                    id="pills-contact-tab"
                    data-bs-toggle="pill"
                    data-bs-target="#pills-bukumimpi3d"
                    type="button"
                    role="tab"
                    aria-controls="pills-bukumimpi3d"
                    aria-selected="false">3D</button>
            </li>
            <li
                on:click={() => {
                    handleClickBukuMimpi("2D");
                }}
                class="nav-item"
                role="presentation">
                <button
                    class="nav-link"
                    id="pills-contact-tab"
                    data-bs-toggle="pill"
                    data-bs-target="#pills-bukumimpi2d"
                    type="button"
                    role="tab"
                    aria-controls="pills-bukumimpi2d"
                    aria-selected="false">2D</button>
            </li>
        </ul>
        <input
            bind:value={searchbukumimpi}
            on:keypress={handleKeyboardbukumimpi_checkenter}
            style="border-radius: none;border: none; background: rgb(48, 48, 48) none repeat scroll 0% 0%; color: white; font-size: {modal_table_fontsize_bukumimpi_header}; "
            placeholder="Ketik apa yang telah kamu mimpikan"
            class="form-control"
            type="text"/>
    </slot:template>
    <slot:template slot="body">
        <div class="tab-content" id="pills-tabContent">
            <div
            class="tab-pane fade show active"
            id="pills-bukumimpiall"
            role="tabpanel"
            aria-labelledby="pills-bukumimpiall-tab">
            {#if filterBukuMimpi != ""}
                <table>
                    <tbody>
                        {#each filterBukuMimpi as rec}
                            <tr>
                                <td
                                    NOWRAP
                                    width="30px"
                                    style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_bukumimpi_header};color:#fc0;">{rec.bukumimpi_tipe}</td>
                                <td
                                    width="*"
                                    style="text-align:left;vertical-align:top;font-size:{modal_table_fontsize_bukumimpi_header};color:#8b8989;">
                                    {rec.bukumimpi_nama}
                                    <br />
                                    <span style="color:#fc0;font-size:{modal_table_fontsize_bukumimpi_header};">{rec.bukumimpi_nomor}</span>
                                </td>
                            </tr>
                        {/each}
                    </tbody>
                </table>
            {:else}
                <Placeholder total_placeholder="10" card_style="background-color:#2c2c2c;border:none;margin-top:5px;" />
            {/if}
            </div>
            <div
                class="tab-pane fade"
                id="pills-bukumimpi4d"
                role="tabpanel"
                aria-labelledby="pills-bukumimpi4d-tab">
                {#if filterBukuMimpi != ""}
                    <table>
                        <tbody>
                            {#each filterBukuMimpi as rec}
                                <tr>
                                    <td
                                        NOWRAP
                                        width="30px"
                                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_bukumimpi_header};color:#fc0;">{rec.bukumimpi_tipe}</td>
                                    <td
                                        width="*"
                                        style="text-align:left;vertical-align:top;font-size:{modal_table_fontsize_bukumimpi_header};color:#8b8989;">
                                        {rec.bukumimpi_nama}
                                        <br />
                                        <span style="color:#fc0;font-size:{modal_table_fontsize_bukumimpi_header};">{rec.bukumimpi_nomor}</span>
                                    </td>
                                </tr>
                            {/each}
                        </tbody>
                    </table>
                {:else}
                    <Placeholder total_placeholder="1-" card_style="background-color:#2c2c2c;border:none;margin-top:5px;" />
                {/if}
            </div>
            <div
                class="tab-pane fade"
                id="pills-bukumimpi3d"
                role="tabpanel"
                aria-labelledby="pills-bukumimpi3d-tab">
                {#if filterBukuMimpi != ""}
                    <table>
                        <tbody>
                            {#each filterBukuMimpi as rec}
                                <tr>
                                    <td
                                        NOWRAP
                                        width="30px"
                                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_bukumimpi_header};color:#fc0;">{rec.bukumimpi_tipe}</td>
                                    <td
                                        width="*"
                                        style="text-align:left;vertical-align:top;font-size:{modal_table_fontsize_bukumimpi_header};color:#8b8989;">
                                        {rec.bukumimpi_nama}
                                        <br />
                                        <span style="color:#fc0;font-size:{modal_table_fontsize_bukumimpi_header};">{rec.bukumimpi_nomor}</span>
                                    </td>
                                </tr>
                            {/each}
                        </tbody>
                    </table>
                {:else}
                    <Placeholder total_placeholder="1-" card_style="background-color:#2c2c2c;border:none;margin-top:5px;" />
                {/if}
            </div>
            <div
                class="tab-pane fade"
                id="pills-bukumimpi2d"
                role="tabpanel"
                aria-labelledby="pills-bukumimpi2d-tab">
                {#if filterBukuMimpi != ""}
                    <table>
                        <tbody>
                            {#each filterBukuMimpi as rec}
                                <tr>
                                    <td
                                        NOWRAP
                                        width="30px"
                                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_bukumimpi_header};color:#fc0;">{rec.bukumimpi_tipe}</td>
                                    <td
                                        width="*"
                                        style="text-align:left;vertical-align:top;font-size:{modal_table_fontsize_bukumimpi_header};color:#8b8989;">
                                        {rec.bukumimpi_nama}
                                        <br />
                                        <span style="color:#fc0;font-size:{modal_table_fontsize_bukumimpi_header};">{rec.bukumimpi_nomor}</span>
                                    </td>
                                </tr>
                            {/each}
                        </tbody>
                    </table>
                {:else}
                    <Placeholder total_placeholder="1-" card_style="background-color:#2c2c2c;border:none;margin-top:5px;" />
                {/if}
            </div>
        </div>
    </slot:template>
</Modal>
<Modal
    modal_id={"modalslipalldetail"}
    modal_footer_flag={true}
    modal_body_height={"height:350px;"}
    modal_size={"modal-dialog-centered"}>
    <slot:template slot="header">
        <h5 class="modal-title">
            PASARAN : {detailslipheader}
        </h5>
    </slot:template>
    <slot:template slot="body">
        <table class="table table-dark table-striped">
            <thead>
                <tr>
                    <th
                        width="1%"
                        style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">NO</th>
                    <th
                        width="15%"
                        style="text-align:left;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">PERMAINAN</th>
                    <th
                        width="50%"
                        style="text-align:right;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">BAYAR</th>
                    <th
                        width="25%"
                        style="text-align:right;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">MENANG</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};">1</td>
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "4D",
                                total4d_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};">4D</td>
                    <td style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};" >
                        {new Intl.NumberFormat().format(total4d_bayar)}
                    </td>
                    <td style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};">
                        {new Intl.NumberFormat().format(totalwin_4d)}
                    </td>
                </tr>
                <tr>
                    <td style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >2</td>
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "3D",
                                total3d_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >3D</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(total3d_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_3d)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >3</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "2D",
                                total2d_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >2D</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(total2d_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_2d)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >4</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "COLOK_BEBAS",
                                totalcolokbebas_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >COLOK BEBAS</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalcolokbebas_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_colokbebas)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >5</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "COLOK_MACAU",
                                totalcolokmacau_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >COLOK MACAU</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalcolokmacau_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_colokmacau)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >6</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "COLOK_NAGA",
                                totalcoloknaga_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >COLOK NAGA</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalcoloknaga_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_coloknaga)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >7</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "COLOK_JITU",
                                totalcolokjitu_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >COLOK JITU</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalcolokjitu_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_colokjitu)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >8</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "50_50_UMUM",
                                total5050umum_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >50 - 50 UMUM</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(total5050umum_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_5050umum)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >9</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "50_50_SPECIAL",
                                total5050special_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >50 - 50 SPECIAL</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(total5050special_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_5050special)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >10</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "50_50_KOMBINASI",
                                total5050kombinasi_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >50 - 50 KOMBINASI</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(
                            total5050kombinasi_bayar
                        )}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_5050kombinasi)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >11</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "MACAU_KOMBINASI",
                                totalmacaukombinasi_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >MACAU / KOMBINASI</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(
                            totalmacaukombinasi_bayar
                        )}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(
                            totalwin_macaukombinasi
                        )}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >12</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "DASAR",
                                totalmacaukombinasi_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >DASAR</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totaldasar_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_dasar)}
                    </td>
                </tr>
                <tr>
                    <td
                        style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};f"
                        >13</td
                    >
                    <td
                        on:click={() => {
                            fetch_invoicealldetailpermainan(
                                "SHIO",
                                totalmacaukombinasi_bayar
                            );
                        }}
                        NOWRAP
                        style="text-decoration:underline;cursor:pointer;text-align:left;vertical-align:top;font-size:{modal_table_fontsize_body};"
                        >SHIO</td
                    >
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalshio_bayar)}
                    </td>
                    <td
                        style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};"
                    >
                        {new Intl.NumberFormat().format(totalwin_shio)}
                    </td>
                </tr>
            </tbody>
        </table>
    </slot:template>
    <slot:template slot="footer">
        <table class="table" width="100%">
            <tr>
                <td
                    NOWRAP
                    width="50%"
                    style="text-align:right;vertical-align:top;color:white;font-size:{modal_table_fontsize_body};"
                    >TOTAL BAYAR</td
                >
                <td
                    NOWRAP
                    width="1%"
                    style="text-align:center;vertical-align:top;color:white;font-size:{modal_table_fontsize_body};"
                    >:</td
                >
                <td
                    NOWRAP
                    width="*"
                    style="text-align:right;vertical-align:top;color:white;font-size:{modal_table_fontsize_body};color:#fc0;"
                    >{new Intl.NumberFormat().format(subtotal_bayar)}</td
                >
            </tr>
            <tr>
                <td
                    NOWRAP
                    style="text-align:right;vertical-align:top;color:white;font-size:12px;"
                    >TOTAL WINNER</td
                >
                <td
                    NOWRAP
                    style="text-align:center;vertical-align:top;color:white;font-size:12px;"
                    >:</td
                >
                <td
                    NOWRAP
                    style="text-align:right;vertical-align:top;color:white;font-size:12px;color:#fc0;"
                    >{new Intl.NumberFormat().format(subtotal_winner)}</td
                >
            </tr>
            <tr>
                <td
                    NOWRAP
                    style="text-align:right;vertical-align:top;color:white;font-size:12px;"
                    >WINLOSE</td
                >
                <td
                    NOWRAP
                    style="text-align:center;vertical-align:top;color:white;font-size:12px;"
                    >:</td
                >
                <td
                    NOWRAP
                    style="text-align:right;vertical-align:top;color:white;font-size:12px;color:#fc0;"
                    >{new Intl.NumberFormat().format(total_winlose)}</td
                >
            </tr>
        </table>
    </slot:template>
</Modal>
<Modal
    modal_id={"modalslipalldetailbyid"}
    modal_footer_flag={true}
    modal_body_height={"height:450px;"}
    modal_size={"modal-lg modal-dialog-centered"}>
    <slot:template slot="header">
        <h5 class="modal-title">
            PERMAINAN : {detailslipheaderpermainan}
        </h5>
    </slot:template>
    <slot:template slot="body">
        <table class="table table-dark">
            <thead>
                <tr>
                    <th width="1%" style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">NO</th>
                    <th width="1%" style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">STATUS</th>
                    <th width="5%" style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">TIPE</th>
                    <th width="20%" style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">PERMAINAN</th>
                    <th width="*" style="text-align:center;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">NOMOR</th>
                    <th width="10%" style="text-align:right;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">BET</th>
                    <th width="10%" style="text-align:right;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">DISC(%)</th>
                    <th width="10%" style="text-align:right;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">KEI(%)</th>
                    <th width="10%" style="text-align:right;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">BAYAR</th>
                    <th width="10%" style="text-align:right;vertical-align:top;background:#303030;font-size:{modal_table_fontsize_header};border-bottom:none;">WIN</th>
                </tr>
            </thead>
            <tbody>
                {#each listhasilinvoicebet as rec}
                    <tr>
                        <td NOWRAP style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};">{rec.bet_no}</td>
                        <td NOWRAP style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};">
                            <span style="padding:5px;border-radius:5px;{rec.bet_background}">{rec.bet_status}</span>
                        </td>
                        <td NOWRAP style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};">{rec.bet_tipe}</td>
                        <td NOWRAP style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};">{rec.bet_permainan}</td>
                        <td NOWRAP style="text-align:center;vertical-align:top;font-size:{modal_table_fontsize_body};">{rec.bet_nomor}</td>
                        <td NOWRAP style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};">
                            {new Intl.NumberFormat().format(rec.bet_bet)}
                        </td>
                        <td NOWRAP style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};">
                            {rec.bet_diskon.toFixed(2)}
                        </td>
                        <td NOWRAP style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};">
                            {rec.bet_kei.toFixed(2)}
                        </td>
                        <td NOWRAP style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};">
                            {new Intl.NumberFormat().format(rec.bet_bayar)}
                        </td>
                        <td NOWRAP style="text-align:right;vertical-align:top;color:#fc0;font-size:{modal_table_fontsize_body};">
                            {new Intl.NumberFormat().format(rec.bet_win)}
                        </td>
                    </tr>
                {/each}
            </tbody>
        </table>
    </slot:template>
</Modal>
<style>
    .table>:not(:first-child) {
         border-top: none; 
    }
</style>