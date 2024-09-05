<template>
  <div>
      <detalle-pelicula :nombre="peliculaSeleccionada"></detalle-pelicula> 
      <tablaPelis :pel="pel" @pelicula-seleccionada="mostrarDetalles"></tablaPelis> 
  </div>
</template>

<script>
import { onMounted, ref } from 'vue';
import TablaPelis from '../components/tablaPelis.vue';
import DetallePelicula from '../components/nombrePeli.vue';

export default {
  name: 'Peliculas',
  components: {
      TablaPelis,
      DetallePelicula 
  },
  setup() {
      const pel = ref([]);
      const peliculaSeleccionada = ref('');

      onMounted(async () => {
          try {
              const response = await fetch('https://dummyapi.online/api/movies');
              const peliculas = await response.json();
              pel.value = peliculas;
          } catch (error) {
              console.log(error);
          }
      });

      const mostrarDetalles = (nombre) => {
          peliculaSeleccionada.value = nombre; 
      };

      return { pel, peliculaSeleccionada, mostrarDetalles };  
  }
};
</script>
