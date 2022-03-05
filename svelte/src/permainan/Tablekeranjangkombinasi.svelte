<script>
    import { Button, Icon } from "sveltestrap";
    import { createEventDispatcher } from "svelte";
    import PanelFull from "../components/Panelfull.svelte";
    import Modal from "../components/Modalfull2.svelte";

    export let keranjang = [];
    export let client_device = "";
    export let totalkeranjang = 0;
    export let group_btn_beli = false;
    export let count_line_macaukombinasi = 0;
    export let count_line_standart = 0;
    export let min_bet = 0;
    export let max_bet = 0;
    export let win_bet = 0;
    export let diskon_bet = 0;

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
    $: count_line = count_line_macaukombinasi + count_line_standart;
</script>

<PanelFull
    header={true}
    footer={true}
    header_style="background:#181717;border-bottom:1px solid #333;border-top: 0 solid #333;"
    body_style="padding:0px;background:#181717;height:500px;">
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
                        <th width="1%" style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>&nbsp;</th>
                        <th width="10%" style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>NOMOR</th>
                        <th width="20%" style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>PERMAINAN</th>
                        <th width="20%" style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>BET</th>
                        <th width="20%" style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>DISKON</th>
                        <th width="*" style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>BAYAR</th>
                    </tr>
                </thead>
                <tbody>
                    {#each keranjang as rec}
                        <tr>
                            <td style="text-align:center;vertical-align:middle;"
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
                        <th width="1%" style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>&nbsp;</th>
                        <th width="10%" style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>NOMOR</th>
                        <th width="20%" style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>PERMAINAN</th>
                        <th width="20%" style="text-align:right;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>BET</th>
                        <th width="20%" style="text-align:right;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>DISKON</th>
                        <th width="*" style="text-align:right;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>BAYAR</th>
                    </tr>
                </thead>
                <tbody>
                    {#each keranjang as rec}
                        <tr>
                            <td style="text-align:center;vertical-align:top;"
                                on:click={() => {
                                    handleRemoveKeranjang(rec.id, rec.bayar);
                                }}>
                                <Icon name="trash" style="cursor:pointer;" />
                            </td>
                            <td style="text-align:center;vertical-align:top;font-size:11px;color:#fc0;">{rec.nomor}</td>
                            <td style="text-align:center;vertical-align:top;font-size:11px;color:#fc0;">{rec.permainan}</td>
                            <td style="text-align:right;vertical-align:top;font-size:11px;color:#fc0;">
                                {new Intl.NumberFormat().format(rec.bet)}
                            </td>
                            <td style="text-align:right;vertical-align:top;font-size:11px;color:#fc0;">
                                {new Intl.NumberFormat().format(
                                    Math.ceil(rec.diskon)
                                )}
                                <br />
                                ({(rec.diskonpercen * 100).toFixed(2)}%)
                            </td>
                            <td style="text-align:right;vertical-align:top;font-size:11px;color:#fc0;">
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
                <td colspan="5" style="color:white;">TOTAL LINE : <span style="color:#f7941d;">{count_line}</span></td>
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
        <h5 class="modal-title">MACAU/KOMBINASI</h5>
    </slot:template>
    <slot:template slot="body">
        <table class="table table-dark table-sm">
            <tbody>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:12px;">MIN BET</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{new Intl.NumberFormat().format(min_bet)}</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:12px;">MAX BET</td >
                    <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{new Intl.NumberFormat().format(max_bet)}</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:12px;">DISKON</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{(diskon_bet * 100).toFixed(2)}%</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:12px;">HADIAH</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#ffd292;">{win_bet.toFixed(2)}x</td>
                </tr>
            </tbody>
        </table>
        <p style="font-size:12px;padding: 5px;color:white;">
            <b>CARA BERMAIN</b>
            <br />
            Struktur ABCD<br /><br />

            AB = DEPAN, BC = TENGAH, CD = BELAKANG<br />
            Besar/Kecil: 0-4=kecil, 5-9=besar<br />
            Ganjil/Genap : 1=ganjil, 2=genap dan seterusnya<br /><br />

            Anda dapat menebak Genap/Ganjil, Besar/Kecil<br />
            dari 2 kombinasi antara DEPAN, TENGAH, BELAKANG<br /><br />

            Analisis : keluar nomor 1845<br /><br />

            berarti pemenang untuk :<br />
            DEPAN Kecil/Genap<br />
            TENGAH Besar/Genap<br />
            BELAKANG Kecil/Ganjil<br /><br />

            Misalnya anda membeli BELAKANG KECIl dan GANJIL seharga 100rb,<br />
            maka menang = 100rb + [indeks kemenangan untuk kombinasi 2]<br />
            atau :<br />
            jika membeli DEPAN KECIL dan GENAP seharga 100rb,<br />
            maka menang = 100rb + [indeks kemenangan untuk kombinasi 2]<br />
            atau :<br />
            jika membeli TENGAH KECIL dan GENAP seharga 100rb, berarti KALAH<br />
            ( Anda harus menebak keduanya dengan Benar diantara DEPAN,TENGAH,BELAKANG agar Menang )<br />
        </p>
    </slot:template>
</Modal>