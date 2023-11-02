<script setup>
import LoadingButton from "./LoadingButton.vue";
import {ref} from 'vue'
// defineProps({
//   header: String,
//   text: String,
//   theme: String
// })
const isLoading =ref(false)
defineProps({
  theme: String,
  email: String

});
const closemodal = () => {

  emit("close");
        isLoading.value = true;
  setTimeout(() => (isLoading.value = false), 100);
};


const emit = defineEmits(["close"]);
defineExpose({ closemodal });
</script>
<template>
  <div>
    <transition name="fade">
    
      <div class="MediaAllContent top-0 left-0 fixed bg-Charcoal_Grey w-full h-full">
        <div class="MediaContents flex h-full justify-center items-center">
          <div class="MediaCildcontents flex flex-col bg-White p-10 gap-y-10 rounded-xl">
            <img class="AlertImage w-10"
            src="../../../images/icon-list.svg" alt="" />
            <h1 class="AlertHead text-6xl font-bold">
              Thanks for
              <br>
              subscribing!
            </h1>
            <p class="AlertParagraph">
              A confirmation email has been sent to 
              <br>
              <strong>
                {{ email }}
              </strong> please open it and click
              <br>
              the button inside to confirm yor subscription.
            </p>
            <LoadingButton
  
            class="AlertButton bg-Charcoal_Grey rounded-md text-White text-center cursor-pointer hover:bg-Tomato"
             @click="closemodal" label="Dismiss message"/>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<style lang="scss" scoped></style>
