<template>
    <div style="margin: 20px 0;">
        <label for="monto">Ingrese monto $ </label>
        <input id="monto" type="number" min="0" :value="monto" @input="onInput" style="font-size:1em;" />
    </div>
</template>

<script>
export default
{
    name: 'ConversorInput',
    props:
    {
        monto:
        {
            type: Number,
            required: true
        }
    },
    
    methods:
    {
        onInput(e)
        {
            const value = Number(e.target.value);
            this.$emit('update:monto', isNaN(value) ? 0 : value);
        }
    }
}
</script>