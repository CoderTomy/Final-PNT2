<template>
    <div style="max-width: 700px; margin: 40px auto;">
        <h1 style="font-size:2em; font-weight:bold;">Conversor Pesos a dólares</h1>
        <ConversorInput :monto="monto" @update:monto="monto = $event" />
            <div v-if="cotizacion">
        <CotizacionInfo :cotizacion="cotizacion" :fechaCotizacion="fechaCotizacion" :valorConvertido="valorConvertido" />
        </div>
        <div v-else style="margin-top:20px; color: #888;">Cargando cotización...</div>
        <hr style="margin-top:30px;" />
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
body
{
    font-family: Arial, Helvetica, sans-serif;
}
</style>