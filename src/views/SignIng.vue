<template>
  <div class="cursor-default text-base">
    <div class="MediaContaner bg-White p-5 pl-16 flex gap-x-20 rounded-xl">
      <img class="MediaImageMobile hidden" src="../../images/illustration-sign-up-mobile.svg" alt="" />
      <div class="MediaChildContaner text-Charcoal_Grey flex flex-col gap-y-8 pt-11">
        <h1 class="text-6xl font-bold m-0">Stay updated!</h1>
        <p>
          Join 60,00+ product managers receicing monthly
          <br />
          updated on:
        </p>
        <ul class="MediaUl flex flex-col gap-y-4">
          <li class="flex gap-x-3">
            <img src="../../images/icon-list.svg" alt="" />
            <p>Measuring to ensure updates are a success</p>
          </li>
          <li class="flex gap-x-3">
            <img src="../../images/icon-list.svg" alt="" />
            <p>And much more!</p>
          </li>
          <li class="flex gap-x-3">
            <img src="../../images/icon-list.svg" alt="" />
            <p>Product discovry and building white matters</p>
          </li>
        </ul>
        <div  class="flex flex-col gap-y-8">
          <label for="" class="flex flex-col gap-y-2">
            <p class="flex justify-between text-sm font-bold">
              <span>Email address</span>
              <span  class="text-Tomato">{{ emailError }}</span>
            </p>
            <!-- In the bind class we say taht if error and emailError it get style other way it not get error   -->
            <input
            
            :class="{'Errorstyle': EmailErrorStyle && emailError }"
              v-model="Email"
              class=" MedaiInput ml-2 pl-6 border-[2.5px] border-Grey/40 font-bold h-12 rounded-md"
              type="emial"
              required
              placeholder="email@company.com"
            />
          </label>
          <transition name="fade">
          
            <LoadingButton
            :disabled="disabled"
              @click="toggleModel"
              :is-loading="isLoading"
              class="MedaiButton ml-2 py-2 text-center text-White bg-Charcoal_Grey rounded-md hover:bg-Tomato"
            >
              Subscribe to monthly newsLetter
            </LoadingButton>
          </transition>
        </div>
        <div v-show="showModel">
          <Alert @close="closeModel" :email="Email" />
        </div>
      </div>
      <img class="MediaImage" src="../../images/illustration-sign-up-desktop.svg" alt="" />

    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import LoadingButton from "./alert/LoadingButton.vue";
import Alert from "./alert/Alert.vue";

const isLoading = ref(false);
const showModel = ref(false);
const Email = ref("");
const emailError = ref('')



const toggleModel = () => {
  const isValidEmail = (Email) => {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  
    return emailRegex.test(Email);
  };

  if (Email.value === '') {
    emailError.value = 'No Email address';
  } else if (isValidEmail(Email.value)) {
    showModel.value = true;
    emailError.value = '';
  } else {
    emailError.value = 'invalid Email';
    Email.value = '';
  }
  isLoading.value = true;
  setTimeout(() => (isLoading.value = false), 100);
};



const closeModel = () => {
showModel.value=false
};
const disabled = computed(() => {
  return Email.value === '';
})

const EmailErrorStyle = computed(() => {
  return emailError.value ;
 })


</script>

<style>
.Errorstyle{
  background-color: rgba(255, 99, 71, 0.262);
  border:2.5px solid rgba(175, 5, 5, 0.342);
  color: rgba(224, 111, 91, 0.828);
  outline-color: rgba(175, 5, 5, 0.342);
}

</style>
