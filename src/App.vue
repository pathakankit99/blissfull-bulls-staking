<template>
  <div class="relative h-full min-h-screen bg-blue-300">
    <TheNavBar />
    <div class="text-blue-800 pt-10 px-10 flex justify-center align-middle text-3xl lg:text-5xl font-bold uppercase">
      <p class=" pt-3 px-1 mt-1">Blissful</p>
      <p class=" pt-3 px-2 mt-1">Bulls</p>
    </div>

    <div class="p-10">
      <router-view />
    </div>

    <div class="pt-10"></div>
  </div>
</template>

<script>
import TheNavBar from "@/components/TheNavBar";
import TheFooter from "@/components/gem-farm/TheFooter";
import TheCat from "@/components/gem-farm/TheCat";
export default {
  components: { TheCat, TheFooter, TheNavBar },
};
</script>

<style>
input[type="radio"]:checked + span {
  @apply text-black;
}
</style>
