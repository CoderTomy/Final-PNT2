<template>
    <div class="input-block">
        <label for="monto" class="input-label">Ingrese monto $</label>
        <input id="monto" type="number" min="0" :value="monto" @input="onInput" class="input-field" />
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

<style scoped>
.input-block
{
    margin: 20px 0 24px 0;
    display: flex;
    align-items: center;
    gap: 12px;
}

.input-label
{
    font-size: 1.08em;
    color: #333;
    font-weight: 500;
}

.input-field
{
    font-size: 1.08em;
    padding: 6px 12px;
    border: 1.2px solid #bdbdbd;
    border-radius: 6px;
    outline: none;
    font-family: 'Roboto', Arial, Helvetica, sans-serif;
    transition: border-color 0.2s;
}

.input-field:focus
{
    border-color: #1976d2;
}
</style>