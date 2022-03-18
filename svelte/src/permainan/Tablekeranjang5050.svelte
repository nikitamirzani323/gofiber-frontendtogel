<script>
    import { Button, Icon, TabContent, TabPane } from "sveltestrap";
    import { createEventDispatcher } from "svelte";
    import PanelFull from "../components/Panelfull.svelte";
    import Modal from "../components/Modalfull2.svelte";

    export let keranjang = [];
    export let client_device = "";
    export let totalkeranjang = 0;
    export let group_btn_beli = false;
    export let count_line_5050umum = 0;
    export let count_line_5050special = 0;
    export let count_line_5050kombinasi = 0;
    export let min_bet_5050umum = 0;
    export let max_bet_5050umum = 0;
    export let keibesar_bet_5050umum = 0;
    export let keikecil_bet_5050umum = 0;
    export let keigenap_bet_5050umum = 0;
    export let keiganjil_bet_5050umum = 0;
    export let keitengah_bet_5050umum = 0;
    export let keitepi_bet_5050umum = 0;
    export let discbesar_bet_5050umum = 0;
    export let disckecil_bet_5050umum = 0;
    export let discgenap_bet_5050umum = 0;
    export let discganjil_bet_5050umum = 0;
    export let disctengah_bet_5050umum = 0;
    export let disctepi_bet_5050umum = 0;
    export let min_bet_5050special = 0;
    export let max_bet_5050special = 0;
    export let keiasganjil_bet_5050special = 0;
    export let keiasgenap_bet_5050special = 0;
    export let keiasbesar_bet_5050special = 0;
    export let keiaskecil_bet_5050special = 0;
    export let keikopganjil_bet_5050special = 0;
    export let keikopgenap_bet_5050special = 0;
    export let keikopbesar_bet_5050special = 0;
    export let keikopkecil_bet_5050special = 0;
    export let keikepalaganjil_bet_5050special = 0;
    export let keikepalagenap_bet_5050special = 0;
    export let keikepalabesar_bet_5050special = 0;
    export let keikepalakecil_bet_5050special = 0;
    export let keiekorganjil_bet_5050special = 0;
    export let keiekorgenap_bet_5050special = 0;
    export let keiekorbesar_bet_5050special = 0;
    export let keiekorkecil_bet_5050special = 0;
    export let discasganjil_bet_5050special = 0;
    export let discasgenap_bet_5050special = 0;
    export let discasbesar_bet_5050special = 0;
    export let discaskecil_bet_5050special = 0;
    export let disckopganjil_bet_5050special = 0;
    export let disckopgenap_bet_5050special = 0;
    export let disckopbesar_bet_5050special = 0;
    export let disckopkecil_bet_5050special = 0;
    export let disckepalaganjil_bet_5050special = 0;
    export let disckepalagenap_bet_5050special = 0;
    export let disckepalabesar_bet_5050special = 0;
    export let disckepalakecil_bet_5050special = 0;
    export let discekorganjil_bet_5050special = 0;
    export let discekorgenap_bet_5050special = 0;
    export let discekorbesar_bet_5050special = 0;
    export let discekorkecil_bet_5050special = 0;
    export let min_bet_5050kombinasi = 0;
    export let max_bet_5050kombinasi = 0;
    export let kei_belakangmono_bet_5050kombinasi = 0;
    export let kei_belakangstereo_bet_5050kombinasi = 0;
    export let kei_belakangkembang_bet_5050kombinasi = 0;
    export let kei_belakangkempis_bet_5050kombinasi = 0;
    export let kei_belakangkembar_bet_5050kombinasi = 0;
    export let kei_tengahmono_bet_5050kombinasi = 0;
    export let kei_tengahstereo_bet_5050kombinasi = 0;
    export let kei_tengahkembang_bet_5050kombinasi = 0;
    export let kei_tengahkempis_bet_5050kombinasi = 0;
    export let kei_tengahkembar_bet_5050kombinasi = 0;
    export let kei_depanmono_bet_5050kombinasi = 0;
    export let kei_depanstereo_bet_5050kombinasi = 0;
    export let kei_depankembang_bet_5050kombinasi = 0;
    export let kei_depankempis_bet_5050kombinasi = 0;
    export let kei_depankembar_bet_5050kombinasi = 0;
    export let disc_belakangmono_bet_5050kombinasi = 0;
    export let disc_belakangstereo_bet_5050kombinasi = 0;
    export let disc_belakangkembang_bet_5050kombinasi = 0;
    export let disc_belakangkempis_bet_5050kombinasi = 0;
    export let disc_belakangkembar_bet_5050kombinasi = 0;
    export let disc_tengahmono_bet_5050kombinasi = 0;
    export let disc_tengahstereo_bet_5050kombinasi = 0;
    export let disc_tengahkembang_bet_5050kombinasi = 0;
    export let disc_tengahkempis_bet_5050kombinasi = 0;
    export let disc_tengahkembar_bet_5050kombinasi = 0;
    export let disc_depanmono_bet_5050kombinasi = 0;
    export let disc_depanstereo_bet_5050kombinasi = 0;
    export let disc_depankembang_bet_5050kombinasi = 0;
    export let disc_depankempis_bet_5050kombinasi = 0;
    export let disc_depankembar_bet_5050kombinasi = 0;

    let count_line = 0;
    let dispatch = createEventDispatcher();

    const handleRemoveKeranjang = (idkeranjang, bayar) => {
        dispatch("removekeranjang", {
            idkeranjang,
            bayar,
        });
    };
    const handleRemoveKeranjang_all = () => {
        dispatch("removekeranjangall", "all");
    };
    const handleSave = () => {
        dispatch("handleSave", "save");
    };
    let open_informasi = false;
    let fullscreen = "";
    const toggle = () => {
        fullscreen = "xl";
        open_informasi = !open_informasi;
    };
    $: count_line =
        count_line_5050umum + count_line_5050special + count_line_5050kombinasi;
</script>

<PanelFull
    header={true}
    footer={true}
    header_style="background:#181717;border-bottom:1px solid #333;border-top: 0 solid #333;"
    body_style="padding:0px;background:#181717;height:470px;">
    <slot:template slot="header">
        {#if client_device == "WEBSITE"}
            {#if group_btn_beli == true}
                <div class="float-end" id="btnbelitogel">
                    <Button
                        id="btn1"
                        data-bs-toggle="modal"
                        data-bs-target="#modalInformasi"
                        style="margin-top:5px;"><Icon name="info-circle" /> Informasi</Button>
                    <Button
                        id="btn1"
                        on:click={handleRemoveKeranjang_all}
                        style="margin-top:5px;"><Icon name="trash" /> Hapus Semua</Button>
                    <Button
                        id="btn1"
                        on:click={handleSave}
                        style="margin-top:5px;"><Icon name="cart-check" /> BELI</Button>
                </div>
            {/if}
            <h1 style="padding:5px;margin:0px;color:white;font-size:15px;">
                TOTAL BAYAR : <span style="color:#fc0;">{new Intl.NumberFormat().format(totalkeranjang)}</span>
            </h1>
        {:else}
            <h1 style="padding:5px;margin:0px;color:white;font-size:13px;">
                TOTAL BAYAR : <span style="color:#fc0;">{new Intl.NumberFormat().format(totalkeranjang)}</span>
            </h1>
            {#if group_btn_beli == true}
                <center id="btnbelitogel">
                    <Button
                        size="sm"
                        id="btn1"
                        data-bs-toggle="modal"
                        data-bs-target="#modalInformasi"
                        style="margin-top:5px;"><Icon name="info-circle" /> Informasi</Button>
                    <Button
                        size="sm"
                        id="btn1"
                        on:click={handleRemoveKeranjang_all}
                        style="margin-top:5px;"><Icon name="trash" /> Hapus Semua</Button>
                    <Button
                        size="sm"
                        id="btn1"
                        on:click={handleSave}
                        style="margin-top:5px;"><Icon name="cart-check" /> BELI</Button>
                </center>
            {/if}
        {/if}
    </slot:template>
    <slot:template slot="body">
        {#if client_device == "WEBSITE"}
            <table class="table table-dark table-striped">
                <thead>
                    <tr>
                        <th
                            width="1%"
                            style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;"
                            NOWRAP>&nbsp;</th>
                        <th
                            width="10%"
                            style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;"
                            NOWRAP>NOMOR</th>
                        <th
                            width="20%"
                            style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;"
                            NOWRAP>PERMAINAN</th>
                        <th
                            width="20%"
                            style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;"
                            NOWRAP>BET</th>
                        <th
                            width="20%"
                            style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;"
                            NOWRAP>DISKON</th>
                        <th
                            width="20%"
                            style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;"
                            NOWRAP>KEI</th>
                        <th
                            width="*"
                            style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;"
                            NOWRAP>BAYAR</th>
                    </tr>
                </thead>
                <tbody>
                    {#each keranjang as rec}
                        <tr>
                            <td
                                style="text-align:center;vertical-align:middle;"
                                on:click={() => {
                                    handleRemoveKeranjang(rec.id, rec.bayar);
                                }}>
                                <Icon name="trash" style="cursor:pointer;" />
                            </td>
                            <td style="text-align:center;vertical-align:top;font-size:12px;color:#fc0;">{rec.nomor}</td>
                            <td style="text-align:center;vertical-align:top;font-size:12px;color:#fc0;">{rec.permainan}</td>
                            <td style="text-align:right;vertical-align:top;font-size:12px;color:#fc0;">
                                {new Intl.NumberFormat().format(rec.bet)}
                            </td>
                            <td style="text-align:right;vertical-align:top;font-size:12px;color:#fc0;">
                                {new Intl.NumberFormat().format(
                                    Math.ceil(rec.diskon)
                                )} ({(rec.diskonpercen * 100).toFixed(2)}%)
                            </td>
                            <td style="text-align:right;vertical-align:top;font-size:12px;color:#fc0;">
                                {new Intl.NumberFormat().format(
                                    Math.ceil(rec.kei)
                                )}
                                ({(rec.kei_percen * 100).toFixed(2)}%)
                            </td>
                            <td style="text-align:right;vertical-align:top;font-size:12px;color:#fc0;">
                                {new Intl.NumberFormat().format(rec.bayar)}
                            </td>
                        </tr>
                    {/each}
                </tbody>
            </table>
        {:else}
            <table class="table table-dark table-striped">
                <thead>
                    <tr>
                        <th
                            width="1%"
                            style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;"
                            NOWRAP>&nbsp;</th>
                        <th
                            width="10%"
                            style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;"
                            NOWRAP>NOMOR</th>
                        <th
                            width="20%"
                            style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;"
                            NOWRAP>PERMAINAN</th>
                        <th
                            width="20%"
                            style="text-align:right;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;"
                            NOWRAP>BET</th>
                        <th
                            width="20%"
                            style="text-align:right;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;"
                            NOWRAP>DISKON</th>
                        <th
                            width="20%"
                            style="text-align:right;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;"
                            NOWRAP>KEI</th>
                        <th
                            width="*"
                            style="text-align:right;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;"
                            NOWRAP>BAYAR</th>
                    </tr>
                </thead>
                <tbody>
                    {#each keranjang as rec}
                        <tr>
                            <td
                                style="text-align:center;vertical-align:top;"
                                on:click={() => {
                                    handleRemoveKeranjang(rec.id, rec.bayar);
                                }}>
                                <Icon name="trash" style="cursor:pointer;" />
                            </td>
                            <td style="text-align:center;vertical-align:top;font-size:11px;color:#ffd292;">{rec.nomor}</td>
                            <td style="text-align:center;vertical-align:top;font-size:11px;color:#ffd292;">{rec.permainan}</td>
                            <td style="text-align:right;vertical-align:top;font-size:11px;color:#ffd292;">
                                {new Intl.NumberFormat().format(rec.bet)}
                            </td>
                            <td style="text-align:right;vertical-align:top;font-size:11px;color:#ffd292;">
                                {new Intl.NumberFormat().format(
                                    Math.ceil(rec.diskon)
                                )}
                                <br />
                                ({(rec.diskonpercen * 100).toFixed(2)}%)
                            </td>
                            <td style="text-align:right;vertical-align:top;font-size:11px;color:#ffd292;">
                                {new Intl.NumberFormat().format(
                                    Math.ceil(rec.kei)
                                )}<br />
                                ({(rec.kei_percen * 100).toFixed(2)}%)
                            </td>
                            <td style="text-align:right;vertical-align:top;font-size:11px;color:#ffd292;">
                                {new Intl.NumberFormat().format(rec.bayar)}
                            </td>
                        </tr>
                    {/each}
                </tbody>
            </table>
        {/if}
    </slot:template>
    <slot:template slot="footer">
        <table
            class="table"
            style="font-size:15px;padding:0px;margin:0px;background:#101010;">
            <tr>
                <td colspan="5" style="color:white;">
                    TOTAL LINE : <span style="color:#fc0;">{count_line}</span>
                </td>
            </tr>
        </table>
    </slot:template>
</PanelFull>

<Modal
    modal_id={"modalInformasi"}
    modal_footer_flag={false}
    modal_body_height={"height:500px;"}
    modal_size={"modal-dialog-centered"}>
    <slot:template slot="header">
        <h5 class="modal-title">50-50</h5>
    </slot:template>
    <slot:template slot="body">
        <TabContent style="padding: 0px;margin:0px;">
            <TabPane
                tabId="informasi_5050umum"
                tab="UMUM"
                active
                style="padding:0px;font-size:12px;color:#8a8a8a;">
                <table class="table table-dark table-sm">
                    <tbody>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">MIN BET</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{new Intl.NumberFormat().format( min_bet_5050umum)}</td>
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">MAX BET</td>
                            <td style="border:1px solid #303030;text-align:right;font-size:12px;color:#ffd292;">{new Intl.NumberFormat().format(max_bet_5050umum)}</td>
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">DISKON</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">
                                BESAR : {(discbesar_bet_5050umum*100).toFixed(2)}% <br />
                                KECIL : {(disckecil_bet_5050umum*100).toFixed(2)}% <br />
                                GENAP : {(discgenap_bet_5050umum*100).toFixed(2)}% <br />
                                GANJIL : {(discganjil_bet_5050umum*100).toFixed(2)}% <br />
                                TENGAH : {(disctengah_bet_5050umum*100).toFixed(2)}% <br />
                                TEPI : {(disctepi_bet_5050umum*100).toFixed(2)}% <br />
                            </td>
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">KEI</td >
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">
                                BESAR : {(keibesar_bet_5050umum*100).toFixed(2)}% <br />
                                KECIL : {(keikecil_bet_5050umum*100).toFixed(2)}% <br />
                                GENAP : {(keigenap_bet_5050umum*100).toFixed(2)}% <br />
                                GANJIL : {(keiganjil_bet_5050umum*100).toFixed(2)}% <br />
                                TENGAH : {(keitengah_bet_5050umum*100).toFixed(2)}% <br />
                                TEPI : {(keitepi_bet_5050umum*100).toFixed(2)}% <br />
                            </td>
                        </tr>
                    </tbody>
                </table>
                <p style="padding: 5px;color:white;font-size:12px;">
                    CARA BERMAIN
                    <br />
                    Permainan ganjil/genap, besar/kecil, dan tengah/ tepi UMUM
                    <br />
                    Struktur: CD ( hanya dua angka belakang yang dihitung)<br /><br />
                    
                    Menebak ganjil/genap dan besar/kecil dari posisi:<br />
                    C=KEPALA<br />
                    D=EKOR<br />
                    Besar/Kecil: 0-4=kecil, 5-9=besar<br />
                    Ganjil/Genap : 1=ganjil, 2=genap dan seterusnya<br /><br />
                    Tengah/Tepi : Tengah: angka 25 s/d 74. TEPI : angka 75 s/d 99, dan 00s/d 24<br /><br />
                    
                    Analisis I :<br />
                    Keluar : 6789, Berarti hasil 89<br />
                    Berarti pemenang adalah yang memilih :<br />
                    BESAR<br />
                    GANJIL<br />
                    TEPI
                </p>
            </TabPane>
            <TabPane
                tabId="informasi_5050special"
                tab="SPECIAL"
                style="padding:0px;font-size:12px;color:#8a8a8a;">
                <table class="table table-dark table-sm">
                    <tbody>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">MIN BET</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{new Intl.NumberFormat().format(min_bet_5050special)}</td>
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">MAX BET</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{new Intl.NumberFormat().format(max_bet_5050special)}</td>
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">DISKON</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">
                                AS GANJIL : {(discasganjil_bet_5050special*100).toFixed(2)}% <br />
                                AS GENAP : {(discasgenap_bet_5050special*100).toFixed(2)}% <br />
                                AS BESAR : {(discasbesar_bet_5050special*100).toFixed(2)}% <br />
                                AS KECIL : {(discaskecil_bet_5050special*100).toFixed(2)}% <br />
                                KOP GANJIL : {(disckopganjil_bet_5050special*100).toFixed(2)}% <br />
                                KOP GENAP : {(disckopgenap_bet_5050special*100).toFixed(2)}% <br />
                                KOP BESAR : {(disckopbesar_bet_5050special*100).toFixed(2)}% <br />
                                KOP KECIL : {(disckopkecil_bet_5050special*100).toFixed(2)}% <br />
                                KEPALA GANJIL : {(disckepalaganjil_bet_5050special*100).toFixed(2)}% <br />
                                KEPALA GENAP : {(disckepalagenap_bet_5050special*100).toFixed(2)}% <br />
                                KEPALA BESAR : {(disckepalabesar_bet_5050special*100).toFixed(2)}% <br />
                                KEPALA KECIL : {(disckepalakecil_bet_5050special*100).toFixed(2)}% <br />
                                EKOR GANJIL : {(discekorganjil_bet_5050special*100).toFixed(2)}% <br />
                                EKOR GENAP : {(discekorgenap_bet_5050special*100).toFixed(2)}% <br />
                                EKOR BESAR : {(discekorbesar_bet_5050special*100).toFixed(2)}% <br />
                                EKOR KECIL : {(discekorkecil_bet_5050special*100).toFixed(2)}% <br />
                            </td>
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">KEI</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">
                                AS GANJIL : {(keiasganjil_bet_5050special*100).toFixed(2)}% <br />
                                AS GENAP : {(keiasgenap_bet_5050special*100).toFixed(2)}% <br />
                                AS BESAR : {(keiasbesar_bet_5050special*100).toFixed(2)}% <br />
                                AS KECIL : {(keiaskecil_bet_5050special*100).toFixed(2)}% <br />
                                KOP GANJIL : {(keikopganjil_bet_5050special*100).toFixed(2)}% <br />
                                KOP GENAP : {(keikopgenap_bet_5050special*100).toFixed(2)}% <br />
                                KOP BESAR : {(keikopbesar_bet_5050special*100).toFixed(2)}% <br />
                                KOP KECIL : {(keikopkecil_bet_5050special*100).toFixed(2)}% <br />
                                KEPALA GANJIL : {(keikepalaganjil_bet_5050special*100).toFixed(2)}% <br />
                                KEPALA GENAP : {(keikepalagenap_bet_5050special*100).toFixed(2)}% <br />
                                KEPALA BESAR : {(keikepalabesar_bet_5050special*100).toFixed(2)}% <br />
                                KEPALA KECIL : {(keikepalakecil_bet_5050special*100).toFixed(2)}% <br />
                                EKOR GANJIL : {(keiekorganjil_bet_5050special*100).toFixed(2)}% <br />
                                EKOR GENAP : {(keiekorgenap_bet_5050special*100).toFixed(2)}% <br />
                                EKOR BESAR : {(keiekorbesar_bet_5050special*100).toFixed(2)}% <br />
                                EKOR KECIL : {(keiekorkecil_bet_5050special*100).toFixed(2)}% <br />
                            </td>
                        </tr>
                    </tbody>
                </table>
                <p style="padding: 5px;color:white;font-size:12px;">
                    CARA BERMAIN
                    <br />
                    Menebak ganjil/genap, besar/kecil <br>
                    Permainan ini sangat menarik karena pasarannya naik turun sesuai keinginan market pada waktu tersebut. Dengan demikian, nilai pembelian dipengaruhi kei (pasaran)
                    <br />
                    Struktur: ABCD<br /><br />
                    
                    Menebak ganjil/genap dan besar/kecil dari posisi:<br />
                    A=AS<br />
                    B=KOP<br />
                    C=KEPALA<br />
                    D=EKOR<br />
                    
                    Besar/Kecil : 0-4=kecil, 5-9=besar<br />
                    Ganjil/Genap : 1=ganjil, 2=genap dan seterusnya<br /><br />
                    
                    Analisis I :<br />
                    Keluar : 4327<br />
                    Berarti pemenang adalah yang memilih :<br />
                    AS GENAP/KECIL<br />
                    KOP GANJIL/KECIL<br />
                    KEPALA GENAP/KECIL<br />
                    EKOR GANJIL/BESAR<br />
                    Misal anda membeli dengan dana Rp.100rb untuk AS Genap, menang = 100rb + [indeks pasaran AS Genap 50-50]<br />
                    Atau :<br />
                    Jika membeli dengan dana Rp.100rb untuk Ekor Ganjil, menang = 100rb + [indeks pasaran Ekor Ganjil 50-50]<br />
                    Atau :<br />
                    Jika membeli dengan dana Rp.100rb untuk AS Ganjil, kalah = 100rb + [indeks pasaran AS Ganjil 50-50]
                </p>
            </TabPane>
            <TabPane
                tabId="informasi_5050kombinasi"
                tab="KOMBINASI"
                style="padding:0px;font-size:12px;color:#8a8a8a;">
                <table class="table table-dark table-sm">
                    <tbody>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">MIN BET</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{new Intl.NumberFormat().format(min_bet_5050kombinasi)}</td >
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">MAX BET</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{new Intl.NumberFormat().format(max_bet_5050kombinasi)}</td>
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">DISKON</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">
                                BELAKANG MONO : {(disc_belakangmono_bet_5050kombinasi*100).toFixed(2)}% <br />
                                BELAKANG STEREO : {(disc_belakangstereo_bet_5050kombinasi*100).toFixed(2)}% <br />
                                BELAKANG KEMBANG : {(disc_belakangkembang_bet_5050kombinasi*100).toFixed(2)}% <br />
                                BELAKANG KEMPIS : {(disc_belakangkempis_bet_5050kombinasi*100).toFixed(2)}% <br />
                                BELAKANG KEMBAR : {(disc_belakangkembar_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH MONO : {(disc_tengahmono_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH STEREO : {(disc_tengahstereo_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH KEMBANG : {(disc_tengahkembang_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH KEMPIS : {(disc_tengahkempis_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH KEMBAR : {(disc_tengahkembar_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN MONO : {(disc_depanmono_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN STEREO : {(disc_depanstereo_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN KEMBANG : {(disc_depankembang_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN KEMPIS : {(disc_depankempis_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN KEMBAR : {(disc_depankembar_bet_5050kombinasi*100).toFixed(2)}% <br />
                            </td>
                        </tr>
                        <tr>
                            <td style="background:#303030;border:1px solid #282828;font-size:12px;">KEI</td>
                            <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;" >
                                BELAKANG MONO : {(kei_belakangmono_bet_5050kombinasi*100).toFixed(2)}% <br />
                                BELAKANG STEREO : {(kei_belakangstereo_bet_5050kombinasi*100).toFixed(2)}% <br />
                                BELAKANG KEMBANG : {(kei_belakangkembang_bet_5050kombinasi*100).toFixed(2)}% <br />
                                BELAKANG KEMPIS : {(kei_belakangkempis_bet_5050kombinasi*100).toFixed(2)}% <br />
                                BELAKANG KEMBAR : {(kei_belakangkembar_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH MONO : {(kei_tengahmono_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH STEREO : {(kei_tengahstereo_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH KEMBANG : {(kei_tengahkembang_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH KEMPIS : {(kei_tengahkempis_bet_5050kombinasi*100).toFixed(2)}% <br />
                                TENGAH KEMBAR : {(kei_tengahkembar_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN MONO : {(kei_depanmono_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN STEREO : {(kei_depanstereo_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN KEMBANG : {(kei_depankembang_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN KEMPIS : {(kei_depankempis_bet_5050kombinasi*100).toFixed(2)}% <br />
                                DEPAN KEMBAR : {(kei_depankembar_bet_5050kombinasi*100).toFixed(2)}% <br />
                            </td>
                        </tr>
                    </tbody>
                </table>
                <p style="padding: 5px;color:white;font-size:12px;">
                    CARA BERMAIN
                    <br />
                    MONO STEREO <br>
                    Menebak dari posisi Depan,Tengah,Belakang.
                    <br />
                    Contoh no 1234<br />
                    Yang dimaksud dengan Posisi Depan adalah 2 no terdepan yaitu 12<br />
                    Yang dimaksud dengan Posisi Tengah adalah 2 no ditengah yaitu 23<br />
                    Yang dimaksud dengan Posisi Belakang adalah 2 no terbelakang yaitu 34<br />
                    STEREO = Terdapat Ganjil dan Genap<br />
                    MONO = Terdapat 1 pasang Ganjil atau 1 pasang Genap<br /><br />
                    
                    Analisis I : Beli Posisi Depan<br />
                    Keluar : 1234<br />
                    Yang menjadi pedoman adalah posisi Depan, berarti 12<br />
                    12 => 1=ganjil dan 2=genap , berarti hasil = STEREO<br /><br />
                    
                    Analisis II : Beli Posisi Tengah<br />
                    Keluar : 4326<br />
                    Yang menjadi pedoman adalah posisi Tengah, berarti 32<br />
                    32 => 3=ganjil dan 2=genap , berarti hasil = STEREO<br /><br />
                    
                    Analisis III : Beli Posisi Belakang<br />
                    Keluar : 4533<br />
                    Yang menjadi pedoman adalah posisi Belakang, berarti 33<br />
                    33 => 3=ganjil dan 3=ganjil , berarti hasil = MONO<br />
                    Jika dilakukan pembelian dengan 100rb dan menang maka: Menang = 100rb + [Indeks kemenangan untuk MONO STEREO]<br /><br />
                    
                    KEMBANG KEMPIS KEMBAR<br />
                    Struktur=ABCD<br />
                    Jika Menebang posisi Depan maka yang menjadi fokus adalah AB<br />
                    Jika Menebang posisi Tengah maka yang menjadi fokus adalah BC<br />
                    Jika Menebang posisi Belakang maka yang menjadi fokus adalah CD<br />
                    KEMBANG jika A &#8249; B ataupun B &#8249; C ataupun C &#8249; D<br />
                    KEMPIS jika A <span style='font-size:12px;'>&#8250</span> B ataupun B <span style='font-size:12px;'>&#8250</span> C ataupun C <span style='font-size:12px;'>&#8250</span> D<br />
                    KEMBAR jika A = B ataupun B = C ataupun C = D<br /><br />
                    
                    Analisis I : Beli Posisi Depan<br />
                    Keluar : 4321<br />
                    Yang menjadi pedoman adalah posisi Depan, berarti 43<br />
                    43 => 4 <span style='font-size:12px;'>&#8250</span>; 3, hasil = KEMPIS<br /><br />

                    Analisis II : Beli Posisi Tengah<br />
                    Keluar : 4236<br />
                    Yang menjadi pedoman adalah posisi Tengah, berarti 23<br />
                    23 => 2 &#8249; 3, hasil = KEMBANG<br /><br />

                    Analisis III : Beli Posisi Belakang:<br />
                    Keluar : 4099<br />
                    Yang menjadi pedoman adalah posisi Belakang, berarti 99<br />
                    99 => Hasil = KEMBAR<br /><br />

                    Jika dilakukan pembelian dengan 100rb dan menang maka:<br />
                    Menang = 100rb + [Indeks kemenangan untuk KEMBANG/KEMPIS/KEMBAR]
                </p>
            </TabPane>
        </TabContent>
    </slot:template>
</Modal>