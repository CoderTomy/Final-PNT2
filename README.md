
# Conversor de Pesos a Dólares - Final PNT2

Este proyecto es una aplicación frontend desarrollada con Vue.js y Vite para el examen final de Programación en Nuevas Tecnologías 2.

## Funcionalidad

- Permite ingresar un monto en pesos argentinos y lo convierte automáticamente a dólares, usando la cotización oficial obtenida en tiempo real desde la API [Bluelytics](https://api.bluelytics.com.ar/v2/latest).
- La cotización se actualiza cada 2 segundos y muestra la fecha y hora de la última actualización.
- Incluye un bloque de respuestas a 5 preguntas de multiple choice sobre Vue.js.

## Estructura del proyecto

- `src/App.vue`: Componente principal, gestiona el estado y la lógica de la app.
- `src/components/ConversorInput.vue`: Componente para el input del monto en pesos.
- `src/components/CotizacionInfo.vue`: Componente para mostrar la cotización, fecha/hora y conversión.
- `src/components/Respuestas.vue`: Componente para mostrar las respuestas de multiple choice.

## Instalación y ejecución

1. Instalar dependencias:
   ```sh
   npm install
   ```
2. Ejecutar en modo desarrollo:
   ```sh
   npm run dev
   ```
3. Compilar para producción:
   ```sh
   npm run build
   ```

## Recomendaciones

- Se recomienda usar [VSCode](https://code.visualstudio.com/) y la extensión [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) para mejor experiencia con Vue 3.

---
Desarrollado para el examen final de PNT2 - Julio 2025
