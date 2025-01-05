<script setup>

    // Macro --> no requieren importarse
    const props = defineProps({
        guitarrax: {
            type: Object,
            required: true,
        }
    })
    

</script>

<template>

    <div class="col-md-6 col-lg-4 my-4 row align-items-center">
        <div class="col-4">
            <img class="img-fluid" v-bind:src="`../../public/img/${guitarrax.imagen}.jpg`" v-bind:alt="`imagen guitarra: ${guitarrax.nombre}`">
        </div>
        <div class="col-8">
            <h3 class="text-black fs-4 fw-bold text-uppercase">{{guitarrax.nombre}}</h3>
            <p>{{ guitarrax.descripcion }}</p>
            <p class="fw-black text-primary fs-3">$ {{ guitarrax.precio }}</p>
            <button 
                type="button"
                class="btn btn-dark w-100 "
            >Agregar al Carrito</button>
        </div>
    </div>

</template>