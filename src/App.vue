<template>
    <div class="app-container">
        <h1 class="main-title">Conversor Pesos a Dólares</h1>
        <ConversorInput :monto="monto" @update:monto="monto = $event" />
        <div v-if="cotizacion">
            <CotizacionInfo :cotizacion="cotizacion" :fechaCotizacion="fechaCotizacion" :valorConvertido="valorConvertido" />
        </div>
        <div v-else class="loading-text">Cargando cotización...</div>
        <hr class="divider" />
        <Respuestas />
    </div>
</template>

<script>
import axios from 'axios';
import ConversorInput from './components/ConversorInput.vue';
import CotizacionInfo from './components/CotizacionInfo.vue';
import Respuestas from './components/Respuestas.vue';

export default
{
    name: 'App',
    components:
    {
        ConversorInput,
        CotizacionInfo,
        Respuestas
    },
    
    data()
    {
        return {
            monto: 0,
            cotizacion: null,
            fechaCotizacion: '',
            timer: null,
        };
    },
    
    computed:
    {
        valorConvertido()
        {
            if (!this.cotizacion) return '0.00';
            const val = this.monto / this.cotizacion;

            return val.toLocaleString('en-US', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
        }
    },
    
    methods:
    {
        async fetchCotizacion()
        {
            try
            {
                const res = await axios.get('https://api.bluelytics.com.ar/v2/latest');
                const valor = res.data.oficial.value_sell;
                this.cotizacion = valor;
                const now = new Date();
                this.fechaCotizacion = `${now.getDate()}/${now.getMonth()+1}/${now.getFullYear()}, ${now.toLocaleTimeString()}`;
            }
            catch (e)
            {
                this.cotizacion = null;
                this.fechaCotizacion = '';
            }
        }
    },
    
    mounted()
    {
        this.fetchCotizacion();
        this.timer = setInterval(this.fetchCotizacion, 2000);
    },
    
    beforeUnmount()
    {
        if (this.timer) clearInterval(this.timer);
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.app-container
{
    max-width: 700px;
    margin: 40px auto;
    background: #f8f9fa;
    border-radius: 12px;
    box-shadow: 0 2px 12px rgba(0,0,0,0.07);
    padding: 32px 28px 24px 28px;
    font-family: 'Roboto', Arial, Helvetica, sans-serif;
}

.main-title
{
    font-size: 2.2em;
    font-weight: 700;
    margin-bottom: 18px;
    color: #222;
    letter-spacing: 0.5px;
}

.divider
{
    margin-top: 30px;
    border: none;
    border-top: 1.5px solid #e0e0e0;
}

.loading-text
{
    margin-top: 20px;
    color: #888;
    font-size: 1.1em;
    font-style: italic;
}
</style>