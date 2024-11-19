<script setup>
import Card from '/src/components/card/Card.vue'
</script>

<template>
  <main>
    <div class="contenedor">
      <div class="items-conatiner">
        <div class="title pb-10">
          <h1 class="text-3xl z-10">Our Collection</h1>
          <p class="z-10">
            Introducing our Coffee Collection, a selection of unique coffees from different roast
            types and origins, expertly roasted in small batches and shipped fresh weekly.
          </p>
          <img src="/vector.svg" alt="" class="absolute z-0 right-auto top-10" />

          <div class="buttons">
            <button class="hover:bg-[#6F757C] w-32 h-10 rounded-lg transition-colors duration-300">
              All Products
            </button>
            <button class="hover:bg-[#6F757C] w-32 h-10 rounded-lg transition-colors duration-300">
              Available Now
            </button>
          </div>
        </div>
        <Card />
      </div>
    </div>
  </main>
</template>

<style scoped>
.title {
  gap: 25px;
  width: 500px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.buttons {
  display: flex;
  flex-direction: row;
  gap: 100px;
}
p {
  display: flex;
  text-align: center;
  color: #6f757c;
  font-weight: 500;
}

.contenedor {
  padding: 10px 30px 40px 30px;
  position: absolute;
  top: 10%;
  left: 10%;
  right: 10%;

  width: 80%;
  height: max-content;
  z-index: 9999;
  border-radius: 20px;
  background-color: #1c1d1f;
}

@media screen and (max-width: 768px) {
  .buttons {
    gap: 10px;
  }
  .title {
    width: 300px;
  }
}
.items-conatiner {
  display: flex;
  height: 90%;

  margin-top: 40px;
  flex-direction: column;
  align-items: center;
}
</style>
