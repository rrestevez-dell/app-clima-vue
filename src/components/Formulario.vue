<script setup>

    import { ref, reactive } from 'vue';
    

    import Alerta from './Alerta.vue'

    const busqueda = reactive({
        ciudad: '',
        pais: ''
    })

    const error = ref('')
    
    const emit = defineEmits(['obtener-clima'])

    const paises = [
      { codigo: 'US', nombre: 'Estados Unidos' },
      { codigo: 'MX', nombre: 'México' },
      { codigo: 'AR', nombre: 'Argentina' },
      { codigo: 'CO', nombre: 'Colombia' },
      { codigo: 'CR', nombre: 'Costa Rica' },
      { codigo: 'ES', nombre: 'España' },
      { codigo: 'PE', nombre: 'Perú' },
      { codigo: 'CU', nombre: 'Cuba'}
    ]


    const consultarClima = () => {
        if (Object.values(busqueda).includes('')) {
            error.value = 'Todos los campos son obligatorios'
            return
        }

        error.value = ''
        emit('obtener-clima', busqueda)
    }

</script>

<template>
    <form 
        class="formulario"
        @submit.prevent="consultarClima"
    >
    <Alerta v-if="error">{{ error }}</Alerta>
        <div class="campo">
            <label for="ciudad">Ciudad</label>
            <input 
                type="text"
                id="ciudad"
                placeholder="Ciudad"
                v-model="busqueda.ciudad"
            >
        </div>

        <div class="campo">
            <label for="pais">Pais</label>
            <select
                id="pais"
                v-model="busqueda.pais"
            >
                <option value="">-- Seleccione un Pais --</option>
                <option v-for="pais in paises" :value="pais.codigo">{{ pais.nombre }}</option>
            </select>
        </div>

        <input type="submit" value="Consultar Clima">
    </form>
</template>
