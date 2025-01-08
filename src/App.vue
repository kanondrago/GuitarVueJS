<script setup>

  import {ref, reactive, onMounted} from 'vue';
  import {db} from './data/guitarras'

  import Header from './components/Header.vue';
  import Guitarra from './components/Guitarra.vue';
  import Footer from './components/Footer.vue';

  const guitarras = ref([]);
  const carrito = ref([]);
  
  onMounted( () => {
    guitarras.value = db;
  })

  const agregarCarrito = (guitarra) => {
    guitarra.cantidad = 1;
    carrito.value.push(guitarra);
    console.log(carrito.value);
  }
  

</script>

<template>

    <Header
      v-bind:carrito="carrito">

    </Header>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
          <Guitarra 
            :key="guitarra.id"
            v-for="guitarra in guitarras"
            v-bind:guitarrax="guitarra"
            v-on:agregar-carrito="agregarCarrito"> 
          </Guitarra>
        </div>

    </main>

    <Footer></Footer>

</template>