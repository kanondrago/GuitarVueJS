<script setup>

  import { ref, reactive, onMounted, watch } from 'vue';
  import { db } from './data/guitarras'

  import Header from './components/Header.vue';
  import Guitarra from './components/Guitarra.vue';
  import Footer from './components/Footer.vue';

  const guitarras = ref([]);
  const carrito = ref([]);
  const guitarra = ref({});

  // Implementación de un watch
  // Esta escuchando cierta funcion o cierto state y cuando cambie, entonces manda a llamar a una función. 
  watch(carrito, () => {
    guardarLocalStorage()
  }, {
    deep: true, // Verificación profunda de igualdad | Tiene implicaciones en el performance cuando se tienen objetos muy grandes
  })
  
  onMounted( () => {
    guitarras.value = db;

    // definiendo un objeto en especifico
    guitarra.value = db[3];

    // recuperando lo del localStorage
    const carritoLocalStorage = localStorage.getItem('carrito')

    if(carritoLocalStorage) {
      carrito.value = JSON.parse(carritoLocalStorage);
    }
  })

  // Guargando en localStorage
  // No se puede almacenar arreglos en localStorage
  const guardarLocalStorage = () => {
    localStorage.setItem('carrito', JSON.stringify(carrito.value));
  }

  const agregarCarrito = (guitarra) => {

    const productoIndex = carrito.value.findIndex(producto => producto.id === guitarra.id);

    if(productoIndex>=0) {
      if(carrito.value[productoIndex].cantidad<5){
        carrito.value[productoIndex].cantidad++;
      }
    } else {
      guitarra.cantidad = 1;
      carrito.value.push(guitarra);
    }

    console.log(carrito.value);
  }

  const aumentarCantidad = (id) => {
    const productoIndex = carrito.value.findIndex(producto => producto.id === id);
    const cantidadGuitarras = carrito.value[productoIndex].cantidad;
    if(cantidadGuitarras < 5) {
      carrito.value[productoIndex].cantidad++;
    }
  }

  const disminuirCantidad = (id) => {
    const productoIndex = carrito.value.findIndex(producto => producto.id === id);
    const cantidadGuitarras = carrito.value[productoIndex].cantidad;
    if(cantidadGuitarras > 1) {
      carrito.value[productoIndex].cantidad--;
    } 
  }

  const eliminarGuitarra = (id) => {
    const productoIndex = carrito.value.findIndex(producto => producto.id === id);
    carrito.value.splice(productoIndex, 1);
  }

  const vaciarCarrito = () => {
    carrito.value = [];
  }

</script>

<template>

    <Header
      v-bind:carrito="carrito"
      v-bind:guitarra="guitarra"
      v-on:aumentar-cantidad="aumentarCantidad"
      v-on:disminuir-cantidad="disminuirCantidad"
      v-on:eliminar-guitarra="eliminarGuitarra"
      v-on:agregar-carrito="agregarCarrito"
      @vaciar-carrito="vaciarCarrito"
      >
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