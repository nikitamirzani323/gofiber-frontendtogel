<script>
  import { Row, Col, Container } from "sveltestrap";
  import Home from "./pages/Home.svelte";
  import Permainan from "./pages/Permainan.svelte";
  import Loader from "./components/Loader.svelte";
  import Notif from "./components/Notif.svelte";
  import dayjs from "dayjs";
  import utc from "dayjs/plugin/utc";
  import timezone from "dayjs/plugin/timezone";

  dayjs.extend(utc);
  dayjs.extend(timezone);

  const queryString = window.location.search;
  const urlParams = new URLSearchParams(queryString);
  const token_browser = urlParams.get("token");
  let client_device = "";
  if (token_browser === null) {
    console.log("TOKEN NOT FOUND");
  } else {
    initTimezone();
  }
  if (
    /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
      navigator.userAgent
    )
  ) {
    // true for mobile device
    client_device = "MOBILE";
  } else {
    client_device = "WEBSITE";
  }

  let listkeluaran = [];
  let pasaran_name = "";
  let pasaran_code = "";
  let pasaran_periode = 0;
  let permainan = "4-3-2";
  let client_token = "";
  let client_company = "";
  let client_username = "";
  let client_ipaddress = "";
  let client_timezone = "";
  let client_website_status = "";
  let client_website_message = "";
  let client_credit = 0;
  const pasaran = (e) => {
    pasaran_code = e.detail.code;
    pasaran_name = e.detail.name;
    pasaran_periode = e.detail.periode;
  };

  let record = "";
  let message_err = "";
  let css_err = "display:none;";
  async function initTimezone() {
    const res = await fetch("/api/healthz");
    if (!res.ok) {
      const message = `An error has occured: ${res.status}`;
      throw new Error(message);
    } else {
      const json = await res.json();
      client_ipaddress = json.real_ip;
      client_timezone = "Asia/Jakarta";
    }
    initapp(token_browser);
  }
  async function initapp(e) {
    const resInit = await fetch("/api/init", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        token: e,
      }),
    });
    if (!resInit.ok) {
      const initMessage = `An error has occured: ${resInit.status}`;
      throw new Error(initMessage);
    } else {
      const initJson = await resInit.json();

      if (initJson.status === 200) {
        switch (initJson.company) {
          case "":
            css_err = "display:inline-block";
            message_err = "Agen not found, Please contact admin";
            setTimeout(function () {
              css_err = "display: none;";
            }, 5000);
            break;
          default:
            client_token = initJson.token;
            client_company = initJson.company;
            client_username = initJson.developer;
            client_credit = initJson.credit;
            client_website_status = initJson.website_status;
            client_website_message = initJson.website_message;
            if (client_website_status == "OFFLINE") {
              client_token = "";
              message_err = client_website_message;
              css_err = "display:inline-block";
            } else {
              initPasaran();
            }
        }
      }
    }
  }
  async function initPasaran() {
    const resPasar = await fetch("/api/listpasaran", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        token: client_token,
        company: client_company,
        timezone: client_timezone,
      }),
    });
    if (!resPasar.ok) {
      const pasarMessage = `An error has occured: ${resPasar.status}`;
      throw new Error(pasarMessage);
    } else {
      const jsonPasar = await resPasar.json();
      if (jsonPasar.status == 200) {
        record = jsonPasar.record;
        if (record != null) {
          for (var i = 0; i < record.length; i++) {
            listkeluaran = [
              ...listkeluaran,
              {
                id: record[i]["pasaran_id"],
                pasaran_code: record[i]["pasaran_id"],
                pasaran: record[i]["pasaran_togel"],
                pasaran_periode: record[i]["pasaran_periode"],
                pasaran_tgl: dayjs(record[i]["pasaran_marketclose"]).tz(client_timezone).format("DD MMM YYYY | HH:mm:ss"),
                pasaran_tglclose: dayjs(record[i]["pasaran_marketclose"]).tz(client_timezone).format("HH:mm:ss"),
                pasaran_tglschedule: dayjs(record[i]["pasaran_marketschedule"]).tz(client_timezone).format("HH:mm:ss"),
                pasaran_tglopen: dayjs(record[i]["pasaran_marketopen"]).tz(client_timezone).format("HH:mm:ss"),
                pasaran_url: record[i]["pasaran_url"],
                pasaran_note: record[i]["pasaran_note"],
                pasaran_status: record[i]["pasaran_status"],
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
  }
</script>

<svelte:head>
  <title>APP TOTO</title>
</svelte:head>
{#if client_device == "WEBSITE"}
  <div class="content" style="margin-top:20px;margin-bottom:50px;">
    <Container>
      {#if token_browser != ""}
        <Row align-items-start>
          {#if pasaran_code != ""}
            {#if client_token != ""}
              <Permainan
                {client_token}
                {client_company}
                {client_username}
                {client_credit}
                {client_ipaddress}
                {client_timezone}
                {client_device}
                {pasaran_code}
                {pasaran_name}
                {pasaran_periode}
                {permainan}
                {listkeluaran}
              />
            {/if}
          {:else if client_token != ""}
            <Home
              {client_token}
              {client_company}
              {client_username}
              {client_credit}
              {client_ipaddress}
              {client_timezone}
              {client_device}
              {listkeluaran}
              on:pasaran={pasaran}
            />
          {:else}
            <Notif message={message_err} css_init={css_err} />
            <div style="height: 100%;margin:100px 0px 100px 0px;">
              <center>
                <Loader cssstyle={"height: 100%;margin:100px 0px 100px 0px;"} />
              </center>
            </div>
          {/if}
        </Row>
      {/if}
    </Container>
  </div>
{:else}
  <Container>
    {#if token_browser != ""}
      <Row align-items-start>
        {#if pasaran_code != ""}
          {#if client_token != ""}
            <Permainan
              {client_token}
              {client_company}
              {client_username}
              {client_credit}
              {client_ipaddress}
              {client_timezone}
              {client_device}
              {pasaran_code}
              {pasaran_name}
              {pasaran_periode}
              {permainan}
            />
          {/if}
        {:else if client_token != ""}
          <Home
            {client_token}
            {client_company}
            {client_username}
            {client_credit}
            {client_ipaddress}
            {client_timezone}
            {client_device}
            {listkeluaran}
            on:pasaran={pasaran}
          />
        {:else}
          <div style="height: 100%;margin:100px 0px 100px 0px;">
            <center>
              <Loader cssstyle={"height: 100%;margin:100px 0px 100px 0px;"} />
            </center>
          </div>
        {/if}
      </Row>
    {/if}
  </Container>
{/if}
