<script setup>

    import { ref, reactive } from 'vue';
    import useClima from '../composables/useClima.js'

    const { formatearTemperatura } = useClima()

    defineProps({
        clima: {
            type: Object,
            required: true
        }
    })

</script>

<template>
    <div class="resultado">
        <h2>Clima de: {{ clima.name }}</h2>
        <P class="actual">{{ formatearTemperatura(clima.main.temp) }} &deg;C</P>
        <div class="temperaturas">
            <p>Min: {{ formatearTemperatura(clima.main.temp_min) }}<span>&deg;C</span></p>
            <p>Max: {{ formatearTemperatura(clima.main.temp_max) }}<span>&deg;C</span></p>
        </div>
        
    </div>
</template>
