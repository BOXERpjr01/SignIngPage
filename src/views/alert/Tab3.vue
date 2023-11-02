<script setup>
import { ref } from 'vue'
import BaTab3 from './BaTab3.vue'
import CLickButton from './button/CLickButton.vue'

const title = ref('My first Vue App')
// const header = ref('Sign up gor the Giveaway!');
// const text = ref('Grab your ninja swag for half price!');

//Show and hide Modal
const showmodal = ref(false)

const toggleShow = () => {
  showmodal.value = !showmodal.value
}
</script>
<template>
  <div>
    <h1 class="text-white text-3xl">{{ title }}</h1>
    <CLickButton @click="toggleShow" label="Open Modal" />
    <div v-if="showmodal" class="felx justify-center items-center">

      <div class="abslute bg-blue-400 left-0  z-30">
        <BaTab3 theme="sale">
          <template v-slot:links>
            <div class="flex gap-4">
              <a href="#">Sign up now</a>
              <a href="">More info</a>
            </div>
          </template>
          <h1 class="text-lightGreen border-none p-0 text-4xl font-bold">Ninja Givaway!</h1>
          <p>Grab your ninja swag for half price!</p>
        </BaTab3>
      </div>
      <!-- <BaTab3 header="Sign up gor the Giveaway!" text="Grab your ninja swag for half price!" /> -->
      <div  @click="toggleShow">
        <div class="top-0 left-0 fixed bg-rgba w-full h-full z-10"></div>
        <!-- <BaTab3 :header="header" :text="text" theme="sale" @click="toggleShow"/> -->
      </div>
    </div>
  </div>
</template>
