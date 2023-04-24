<script setup lang="ts">
import { reactive, ref, computed, watch } from "vue";
import { TransitionRoot } from "@headlessui/vue";

const data: any = reactive([
  {
    id: 0,
    img: "https://images.pexels.com/photos/13962287/pexels-photo-13962287.png?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
  },
  {
    id: 1,
    img: "https://images.pexels.com/photos/15893600/pexels-photo-15893600.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
  },
  {
    id: 2,
    img: "https://images.pexels.com/photos/16401371/pexels-photo-16401371.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
  },
]);

const selectedItem: Number = ref(0);
const prevSelectedItem: Number = ref(0);

watch(selectedItem, (current, prev) => {
  prevSelectedItem.value = prev;
});
</script>

<template>
  <div class="container mx-auto">
    <div v-for="(d, index) in data" :key="index" class="relative">
      <div
        class="absolute z-30 flex space-x-3 -translate-x-1/2 bottom-5 left-1/2"
      >
        <button
          type="button"
          :class="`w-3 h-3 rounded-full ${
            selectedItem === btnIndex ? 'bg-black' : 'bg-gray-500'
          }`"
          v-for="(d, btnIndex) in data"
          :key="d.id"
          @click="selectedItem = btnIndex"
        ></button>
      </div>

      <TransitionRoot
        :show="selectedItem === index"
        :enter="`transform transition ease-in-out duration-300 sm:duration-700`"
        :enter-from="`${
          selectedItem < prevSelectedItem ? '-' : ''
        }translate-x-full`"
        :enter-to="`${selectedItem < prevSelectedItem ? '-' : ''}translate-x-0`"
        leave="transform transition ease-in-out duration-300 sm:duration-700"
        :leave-from="`${
          selectedItem < prevSelectedItem ? '-' : ''
        }translate-x-0`"
        :leave-to="`${
          selectedItem < prevSelectedItem ? '-' : ''
        }translate-x-full`"
      >
        <img v-show="selectedItem === index" :src="d.img" />
      </TransitionRoot>
    </div>
  </div>
</template>
