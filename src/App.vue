<script setup>

  import {ref, reactive, onMounted} from 'vue';
  import {db} from './data/guitarras'

  import Header from './components/Header.vue';
  import Guitarra from './components/Guitarra.vue';

  const guitarras = ref([]);
  
  onMounted( () => {
    guitarras.value = db;
  })
  

</script>

<template>

    <Header></Header>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
          <Guitarra 
            :key="guitarra.id"
            v-for="guitarra in guitarras"
            v-bind:guitarrax="guitarra"> 
          </Guitarra>
        </div>

    </main>

    <footer class="bg-dark mt-5 py-5">
        <div class="container-xl">
            <p class="text-white text-center fs-4 mt-4 m-md-0">GuitarLA - Todos los derechos Reservados</p>
        </div>
    </footer>

</template>