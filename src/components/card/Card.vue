<template>
  <div>
    <!-- Mensaje de carga -->
    <div v-if="isLoading" class="grid xl:grid-cols-3 md:grid-cols-2 gap-10 mt-10 sm:grid-cols-1 relative">
      <Skeleton/>
      <Skeleton/>
      <Skeleton/>
      <Skeleton/>
      <Skeleton/>
      <Skeleton/>
    </div>

    <!-- Grid de elementos cuando los datos están listos -->
    <div
      v-else
      class="grid xl:grid-cols-3 md:grid-cols-2 gap-10 mt-10 sm:grid-cols-1 relative"
    >
      <div v-for="item in datos" :key="item.id">
        <div class="relative cursor-pointer hover:scale-105 duration-300">
          <div
            class="popular p-1 text-center w-20 bg-[#F6C768] text-[#111315] font-bold rounded-xl"
            v-if="item.popular"
          >
            <p>Popular</p>
          </div>
          <img
            :src="item.image"
            alt=""
            class="w-80 object-cover relative rounded-md"
          />
        </div>

        <div class="footer-card flex justify-between mt-5">
          <h1 class="text-[#FEF7EE] font-semibold">{{ item.name }}</h1>
          <span
            class="w-14 bg-[#BEE3CC] text-black font-bold text-center rounded-md text-sm p-1"
          >
            {{ item.price }}
          </span>
        </div>
        <div class="ratin flex gap-2 mt-2 relative">
          <div class="flex" v-if="vote(item.votes)">
            <img src="/public/Star_fill.svg" alt="" />
            <p>
              {{ item.rating }}
              <span class="text-gray-500 font-semibold"
                >({{ item.votes }} votes)</span
              >
            </p>
          </div>
          <div class="flex" v-else>
            <img src="/public/Star.svg" alt="" />
            <p>
              {{ item.rating }}
              <span class="text-gray-500 font-semibold">No ratings</span>
            </p>
          </div>
          <p
            class="text-red-500 font-bold absolute right-0"
            v-if="!item.available"
          >
            Sold out
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Skeleton from "/src/components/skeleton/Skeleton.vue";

import { ref, onMounted } from 'vue'

const URL =
  'https://raw.githubusercontent.com/devchallenges-io/web-project-ideas/main/front-end-projects/data/simple-coffee-listing-data.json'

// Variables reactivas
const datos = ref(null) // Para almacenar los datos
const isLoading = ref(true) // Estado de carga

// Función para cargar imágenes
const loadImages = async (data) => {
  const imagePromises = data.map((item) => {
    return new Promise((resolve) => {
      const img = new Image()
      img.src = item.image
      img.onload = resolve
      img.onerror = resolve
    })
  })

  await Promise.all(imagePromises)
}

// Función para obtener los datos
async function getData() {
  try {
    const response = await fetch(URL)
    const data = await response.json()

    // Cargar imágenes antes de mostrar los datos
    await loadImages(data)

    // Actualizar datos y estado de carga
    datos.value = data
    isLoading.value = false
  } catch (error) {
    console.error(error)
    isLoading.value = false
  }
}

// Función de votación
const vote = (item) => item !== 0

onMounted(() => {
  getData() // Llamar a la función para obtener los datos cuando el componente se monta
})
</script>


<style scoped>
.popular {
  position: absolute;
  top: 10px;
  left: 12px;
  z-index: 141414;
}

.card {
  padding: 5px;
  width: 350px;
  height: 200px;
  background-color: rgb(255, 235, 205);
  border-radius: 10px;
}
</style>
