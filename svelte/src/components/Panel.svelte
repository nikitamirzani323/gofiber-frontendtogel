<script>
    import { Card, CardBody, CardHeader } from "sveltestrap";
</script>

<Card color="dark" style="border:1px solid #262424;">
    <CardHeader style="background:#2f2e2e;border-bottom:1px solid #333;border-top: 0 solid #333;">
        <slot name="header" />
    </CardHeader>
    <CardBody style="background:#121212;padding:10px;margin:0px;">
        <slot name="body" />
    </CardBody>
</Card>
