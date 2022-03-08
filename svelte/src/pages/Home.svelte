<script>
    import { createEventDispatcher } from "svelte";
    import { Card, CardBody, CardHeader, CardFooter, Col } from "sveltestrap";
    import Header from "../components/Header.svelte";

    export let client_token = "";
    export let client_company = "";
    export let client_username = "";
    export let client_credit = 0;
    export let client_ipaddress = "";
    export let client_timezone = "Asia/Jakarta";
    export let client_device = "";
    export let listkeluaran = [];
    let dispatch = createEventDispatcher();

    const handleClick = (code, name, periode, status) => {
        if (status == "ONLINE") {
            const pasaran = {
                code,
                periode,
                name,
                client_token,
            };
            dispatch("pasaran", pasaran);
        } else {
            alert("PASARAN " + name + " OFFLINE");
        }
    };
</script>

<Header
    {client_username}
    {client_company}
    {client_credit}
    {client_token}
    {client_ipaddress}
    {client_timezone}
    {client_device}/>
    {#each listkeluaran as rec}
        {#if client_device == "WEBSITE"}
            <Col
                xxl="3"
                xl="3"
                lg="6"
                md="6"
                sm="6"
                xs="6"
                style="cursor:pointer;padding:5px;margin:0px;">
                <Card
                    color="dark"
                    style="border:none;background:#181a1c;"
                    on:click={() => {
                        handleClick(
                            rec.pasaran_code,
                            rec.pasaran,
                            rec.pasaran_periode,
                            rec.pasaran_status
                        );
                    }}>
                    <CardHeader style="background:#181a1c;border:none;">
                        <center id="style_text" style="font-size:18px;">
                            {rec.pasaran}
                        </center>
                    </CardHeader>
                    <CardBody style="background:#181a1c;border:none;">
                        <div class="float-end">
                            {#if rec.pasaran_status == "ONLINE"}
                                <div class="blink_me" style="margin-top:5px;color:black;background:#c4f750;font-size:11px;font-weight:bold;padding:5px;border-radius:5px">
                                    {rec.pasaran_status}
                                </div>
                            {:else}
                                <div style="margin-top:5px;background:#f7602e;color:white;font-size:11px;font-weight:bold;padding:5px;border-radius:5px">
                                    {rec.pasaran_status}
                                </div>
                            {/if}
                        </div>
                        <span style="font-size: 12px;">PERIODE : {rec.pasaran_periode}</span><br />
                        <span style="font-size: 11px;">{rec.pasaran_tgl} WIB</span>
                    </CardBody>
                </Card>
            </Col>
        {:else}
            <Col
                xxl="6"
                xl="6"
                lg="6"
                md="6"
                sm="6"
                xs="6"
                style="cursor:pointer;padding:5px;margin:0px;">
                <Card
                    color="dark"
                    style="border:none;background:#181a1c;"
                    on:click={() => {
                        handleClick(
                            rec.pasaran_code,
                            rec.pasaran,
                            rec.pasaran_periode,
                            rec.pasaran_status
                        );
                    }}>
                    <CardHeader style="background:#181a1c;border:none;">
                        <center id="style_text" style="font-size:15px;">
                            {rec.pasaran}
                        </center>
                    </CardHeader>
                    <CardBody style="background:#181a1c;border:none;">
                        <span style="font-size: 11px;">
                            PERIODE : {rec.pasaran_periode}
                        </span>
                        <br />
                        <span style="font-size: 10px;">{rec.pasaran_tgl} WIB</span>
                    </CardBody>
                    <CardFooter style="padding:0px;margin:0px;">
                        {#if rec.pasaran_status == "ONLINE"}
                            <div
                                class="blink_me"
                                style="margin-top:0px;color:black;background:#c4f750;font-size:12px;font-weight:bold;padding:5px;border-radius:0px;text-align:center;"
                            >
                                {rec.pasaran_status}
                            </div>
                        {:else}
                            <div
                                style="margin-top:0px;background:#f7602e;color:white;font-size:12px;font-weight:bold;padding:5px;border-radius:0px;text-align:center;"
                            >
                                {rec.pasaran_status}
                            </div>
                        {/if}
                    </CardFooter>
                </Card>
            </Col>
        {/if}
    {/each}

<div class="clearfix" />
<br />

<style>
    .blink_me {
        animation: blinker 1s linear infinite;
    }

    @keyframes blinker {
        50% {
            opacity: 0;
        }
    }
</style>
