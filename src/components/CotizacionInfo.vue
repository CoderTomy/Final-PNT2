<template>
    <div class="cotizacion-block">
        <div class="cotizacion-row">
            <span class="cotizacion-label">Valor del dólar oficial venta</span>
            <span class="cotizacion-value">${{ cotizacion }}</span>
            <span class="cotizacion-date">- fecha: <i>{{ fechaCotizacion }}</i></span>
        </div>
        <div class="convertido-row">
            Valor convertido <span class="convertido-value">USD {{ valorConvertido }}</span>
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

<style scoped>
.cotizacion-block
{
    margin-bottom: 18px;
}

.cotizacion-row
{
    margin-bottom: 8px;
    font-size: 1.08em;
    color: #222;
    display: flex;
    align-items: center;
    gap: 10px;
}

.cotizacion-label
{
    font-weight: 500;
}

.cotizacion-value
{
    font-weight: 700;
    color: #1976d2;
    font-size: 1.13em;
}

.cotizacion-date
{
    color: #666;
    font-size: 0.98em;
}

.convertido-row
{
    font-size: 1.12em;
    margin-top: 6px;
}

.convertido-value
{
    font-weight: 700;
    color: #388e3c;
    margin-left: 4px;
}
</style>