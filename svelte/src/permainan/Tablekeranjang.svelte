<script>
    import { Button, Icon } from "sveltestrap";
    import { createEventDispatcher } from "svelte";
    import PanelFull from "../components/Panelfull.svelte";
    import Modal from "../components/Modalfull2.svelte";

    export let keranjang = [];
    export let totalkeranjang = 0;
    export let client_device = "";
    export let group_btn_beli = false;
    export let count_line_4d = 0;
    export let count_line_3d = 0;
    export let count_line_3dd = 0;
    export let count_line_2d = 0;
    export let count_line_2dd = 0;
    export let count_line_2dt = 0;
    export let minimal_bet = 0;
    export let max4d_bet = 0;
    export let max3d_bet = 0;
    export let max3dd_bet = 0;
    export let max2d_bet = 0;
    export let max2dd_bet = 0;
    export let max2dt_bet = 0;
    export let disc4d_bet = 0;
    export let disc3d_bet = 0;
    export let disc3dd_bet = 0;
    export let disc2d_bet = 0;
    export let disc2dd_bet = 0;
    export let disc2dt_bet = 0;
    export let win4d_bet = 0;
    export let win3d_bet = 0;
    export let win3dd_bet = 0;
    export let win2d_bet = 0;
    export let win2dd_bet = 0;
    export let win2dt_bet = 0;
    export let win4dnodiskon_bet = 0;
	export let win3dnodiskon_bet = 0;
	export let win3ddnodiskon_bet = 0;
	export let win2dnodiskon_bet = 0;
	export let win2ddnodiskon_bet = 0;
	export let win2dtnodiskon_bet = 0;
    export let win4dbb_kena_bet = 0;
    export let win3dbb_kena_bet = 0;
    export let win3ddbb_kena_bet = 0;
    export let win2dbb_kena_bet = 0;
    export let win2ddbb_kena_bet = 0;
    export let win2dtbb_kena_bet = 0;
    export let win4dbb_bet = 0;
    export let win3dbb_bet = 0;
    export let win3ddbb_bet = 0;
    export let win2dbb_bet = 0;
    export let win2ddbb_bet = 0;
    export let win2dtbb_bet = 0;
    export let limitline_4d = 0;
    export let limitline_3d = 0;
    export let limitline_3dd = 0;
    export let limitline_2d = 0;
    export let limitline_2dd = 0;
    export let limitline_2dt = 0;

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
        count_line_4d +
        count_line_3d +
        count_line_3dd +
        count_line_2d +
        count_line_2dd +
        count_line_2dt;
</script>

<PanelFull
    header={true}
    footer={true}
    header_style="background:#181717;border-bottom:1px solid #333;border-top: 0 solid #333;"
    body_style="padding:0px;background:#181717;height:450px;">
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
            <br />
            {#if group_btn_beli == true}
                <center id="btnbelitogel">
                    <Button
                        id="btn1"
                        size="sm"
                        data-bs-toggle="modal"
                        data-bs-target="#modalInformasi"
                        style="margin-top:5px;"><Icon name="info-circle" /> Informasi</Button>
                    <Button
                        id="btn1"
                        size="sm"
                        on:click={handleRemoveKeranjang_all}
                        style="margin-top:5px;"><Icon name="trash" /> Hapus Semua</Button>
                    <Button
                        id="btn1"
                        size="sm"
                        on:click={handleSave}
                        style="margin-top:5px;"><Icon name="cart-check" /> BELI</Button>
                </center>
            {/if}
        {/if}
    </slot:template>
    <slot:template slot="body">
        {#if client_device == "WEBSITE"}
            <table class="table table-dark table-striped table-sm">
                <thead>
                    <tr>
                        <th width="1%" style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>&nbsp;</th>
                        <th width="10%" style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>NOMOR</th>
                        <th width="10%" style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>TIPE</th>
                        <th width="20%" style="text-align:center;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>PERMAINAN</th>
                        <th width="20%" style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>BET</th>
                        <th width="20%" style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>DISKON</th>
                        <th width="*" style="text-align:right;vertical-align:top;background:#303030;font-size:13px;border-bottom:none;" NOWRAP>BAYAR</th>
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
                            <td style="text-align:center;vertical-align:top;font-size:12px;color:white;">{rec.nomor}</td>
                            <td style="text-align:center;vertical-align:top;font-size:12px;color:white;">{rec.tipetoto}</td>
                            <td style="text-align:center;vertical-align:top;font-size:12px;color:white;">{rec.permainan}</td>
                            <td style="text-align:right;vertical-align:top;font-size:12px;color:#fc0;">{new Intl.NumberFormat().format(rec.bet)}</td>
                            <td style="text-align:right;vertical-align:top;font-size:12px;color:#fc0;">{new Intl.NumberFormat().format( Math.ceil(rec.diskon))} ({(rec.diskonpercen * 100).toFixed(2)}%)</td>
                            <td style="text-align:right;vertical-align:top;font-size:12px;color:#fc0;">{new Intl.NumberFormat().format(rec.bayar)}</td>
                        </tr>
                    {/each}
                </tbody>
            </table>
        {:else}
            <div style="margin:5px">
                <table class="table table-dark table-striped">
                    <thead>
                        <tr>
                            <th width="1%" style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>&nbsp;</th>
                            <th width="10%" style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>NOMOR</th>
                            <th width="10%" style="text-align:center;vertical-align:top;background:#303030;font-size:11px;border-bottom:none;" NOWRAP>TIPE</th>
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
                                        handleRemoveKeranjang(
                                            rec.id,
                                            rec.bayar
                                        );
                                    }}>
                                    <Icon
                                        name="trash"
                                        style="cursor:pointer;"/>
                                </td>
                                <td style="text-align:center;vertical-align:top;font-size:11px;color:white;">{rec.nomor}</td>
                                <td style="text-align:center;vertical-align:top;font-size:11px;color:white;">{rec.tipetoto}</td>
                                <td style="text-align:center;vertical-align:top;font-size:11px;color:white;">{rec.permainan}</td>
                                <td style="text-align:right;vertical-align:top;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(rec.bet)}</td>
                                <td style="text-align:right;vertical-align:top;font-size:11px;color:#fc0;">
                                    {new Intl.NumberFormat().format( Math.ceil(rec.diskon))} <br />
                                    ({(rec.diskonpercen * 100).toFixed(2)}%)
                                </td>
                                <td style="text-align:right;vertical-align:top;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(rec.bayar)}</td>
                            </tr>
                        {/each}
                    </tbody>
                </table>
            </div>
        {/if}
    </slot:template>
    <slot:template slot="footer">
        {#if client_device == "WEBSITE"}
            <table
                class="table"
                style="font-size:15px;padding:0px;margin:0px;background:#101010;">
                <tr>
                    <td colspan="5" style="color:white;">TOTAL LINE : <span style="color:#fc0;">{count_line}</span></td>
                </tr>
                <tr>
                    <td style="color:white;">4D : <span style="color:#fc0;">{count_line_4d}</span></td>
                    <td style="color:white;">3D : <span style="color:#fc0;">{count_line_3d}</span></td>
                    <td style="color:white;">3D DEPAN : <span style="color:#fc0;">{count_line_3dd}</span></td>
                    <td style="color:white;">2D : <span style="color:#fc0;">{count_line_2d}</span></td>
                    <td style="color:white;">2D DEPAN : <span style="color:#fc0;">{count_line_2dd}</span></td>
                    <td style="color:white;">2D TENGAH : <span style="color:#fc0;">{count_line_2dt}</span></td>
                </tr>
            </table>
        {:else}
            <table
                class="table"
                style="font-size:12px;padding:0px;margin:0px;background:#101010;">
                <tr>
                    <td colspan="5" style="color:white;">TOTAL LINE : <span style="color:#fc0;">{count_line}</span></td>
                </tr>
                <tr>
                    <td style="color:white;">4D : <span style="color:#fc0;">{count_line_4d}</span></td>
                    <td style="color:white;">3D : <span style="color:#fc0;">{count_line_3d}</span></td>
                    <td style="color:white;">3D DEPAN : <span style="color:#fc0;">{count_line_3d}</span></td>
                    <td style="color:white;">2D : <span style="color:#fc0;">{count_line_2d}</span></td>
                    <td style="color:white;">2D DEPAN : <span style="color:#fc0;">{count_line_2dd}</span></td>
                    <td style="color:white;">2D TENGAH : <span style="color:#fc0;">{count_line_2dt}</span></td>
                </tr>
            </table>
        {/if}
    </slot:template>
</PanelFull>

<Modal
    modal_id={"modalInformasi"}
    modal_footer_flag={false}
    modal_body_height={"height:500px;"}
    modal_size={"modal-dialog-centered"}>
    <slot:template slot="header">
        <h5 class="modal-title">4D, 3D dan 2D</h5>
    </slot:template>
    <slot:template slot="body">
        <table class="table table-dark">
            <thead>
                <tr>
                    <th style="background:#303030;border:1px solid #282828;border-bottom:none;">&nbsp;</th>
                    <th style="background:#303030;border:1px solid #282828;text-align:right;border-bottom:none;font-size:11px;">4D</th>
                    <th style="background:#303030;border:1px solid #282828;text-align:right;border-bottom:none;font-size:11px;">3D</th>
                    <th style="background:#303030;border:1px solid #282828;text-align:right;border-bottom:none;font-size:11px;">3DD / 3D DEPAN</th>
                    <th style="background:#303030;border:1px solid #282828;text-align:right;border-bottom:none;font-size:11px;">2D</th>
                    <th style="background:#303030;border:1px solid #282828;text-align:right;border-bottom:none;font-size:11px;">2DD / 2D DEPAN</th>
                    <th style="background:#303030;border:1px solid #282828;text-align:right;border-bottom:none;font-size:11px;">2DT / 2D TENGAH</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td nowrap style="background:#303030;border:1px solid #282828;font-size:12px;">MIN BET</td>
                    <td nowrap style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(minimal_bet)}</td>
                    <td nowrap style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(minimal_bet)}</td>
                    <td nowrap style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format( minimal_bet)}</td>
                    <td nowrap style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(minimal_bet)}</td>
                    <td nowrap style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(minimal_bet)}</td>
                    <td nowrap style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(minimal_bet)}</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:11px;">MAX BET</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(max4d_bet)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(max3d_bet)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(max3dd_bet)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(max2d_bet)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(max2dd_bet)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(max2dt_bet)}</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:11px;">DISKON</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{(disc4d_bet * 100).toFixed(2)}%</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{(disc3d_bet * 100).toFixed(2)}%</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{(disc3dd_bet * 100).toFixed(2)}%</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{(disc2d_bet * 100).toFixed(2)}%</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{(disc2dd_bet * 100).toFixed(2)}%</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{(disc2dt_bet * 100).toFixed(2)}%</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:11px;">HADIAH</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win4d_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win3d_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win3dd_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2d_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2dd_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2dt_bet}x</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:11px;">HADIAH FULL</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win4dnodiskon_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win3dnodiskon_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win3ddnodiskon_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2dnodiskon_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2ddnodiskon_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2dtnodiskon_bet}x</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:11px;" NOWRAP>HADIAH BB KENA</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win4dbb_kena_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win3dbb_kena_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win3ddbb_kena_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2dbb_kena_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2ddbb_kena_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2dtbb_kena_bet}x</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:11px;">HADIAH BB</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:12px;color:#fc0;">{win4dbb_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win3dbb_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win3ddbb_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2dbb_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2ddbb_bet}x</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{win2dtbb_bet}x</td>
                </tr>
                <tr>
                    <td style="background:#303030;border:1px solid #282828;font-size:11px;">LIMIT LINE</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(limitline_4d)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(limitline_3d)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(limitline_3dd)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(limitline_2d)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(limitline_2dd)}</td>
                    <td style="border:1px solid #282828;text-align:right;font-size:11px;color:#fc0;">{new Intl.NumberFormat().format(limitline_2dt)}</td>
                </tr>
            </tbody>
        </table>
        <p style="font-size:12px;padding:5px;color:white;">
            <b>Contoh Penulisan 4D/3D/2D:</b><br />
            1234 : 4D<br /> 
            123 : 3D<br /> 
            *123 : 3D<br /> 
            123* : 3DD / 3D DEPAN<br /> 
            12 : 2D <br />
            **12 : 2D<br /> 
            12** : 2DD / 2D DEPAN<br /> 
            *12* : 2DT / 2D TENGAH
        </p>
        <p style="font-size:12px;padding: 5px;color:white;">
            <b>CARA BERMAIN</b><br>
            Menebak 4 angka, 3 angka dan 2 angka
            <br />
            Struktur ABCD<br /><br />

            Misalnya keluar : 4321<br />
            Berarti pemenang untuk<br />
            4D = 4321<br />
            3D = 321<br />
            3DD / 3D DEPAN = 432<br />
            2D = 21<br />
            2DD / 2D DEPAN = 43<br />
            2DT / 2D TENGAH = 32<br /><br />

            Aturan permainan:<br />
            1. Jika anda membeli diluar dari nomor yang dikeluarkan, berarti
            anda kalah dan uang tidak dikembalikan sama sekali.<br />
            2. Jika anda membeli masing 100rb untuk angka :<br />
            4D = 4321<br />
            3D = 321<br />
            2D = 21<br /><br />
            Berarti kemenangan anda adalah :<br />
            4D = 100rb x [Indeks kemenangan untuk 4D]<br />
            3D = 100rb x [Indeks kemenangan untuk 3D]<br />
            2D = 100rb x [Indeks kemenangan untuk 2D]<br /><br />
            (Catatan: nilai bet 100rb tidak dikembalikan ke member)<br/>
            (Khusus untuk 4D,3D dan 2D diberikan diskon tambahan)<br />
        </p>
    </slot:template>
</Modal>