<template>
    <div>
        <div style="margin-bottom:10px;">
            Valor del dolar oficial venta <b>${{ cotizacion }}</b> - fecha: <i>{{ fechaCotizacion }}</i>
        </div>
        <div>
            Valor convertido <b>USD {{ valorConvertido }}</b>
        </div>
    </div>
</template>

<script>
export default
{
    name: 'CotizacionInfo',
    props:
    {
        cotizacion:
        {
            type: Number,
            required: true
        },
        fechaCotizacion:
        {
            type: String,
            required: true
        },
        valorConvertido:
        {
            type: String,
            required: true
        }
    }
}
</script>