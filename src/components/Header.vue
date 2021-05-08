<template>
  <header
    class="bg-green-600 p-4 flex justify-start sm:justify-center items-center"
  >
    <div class="flex flex-col">
      <h1 class="text-white text-3xl md:text-4xl font-semibold mb-2">
        <i class="fas fa-head-side-mask"></i>
        Covid-Status
      </h1>
    </div>

    <div class="absolute right-10" @click="closeInfo()">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6 text-white hover:text-green-300 transition cursor-pointer"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor">
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
      </svg>
    </div>

    <!-- Info Dropdown Content -->
    <div
      v-if="isHidden == false"
      class="right-8 absolute top-14 space-y-2 bg-white dark:bg-gray-800 p-6 rounded-lg shadow-lg">
      
      <p class="text text-right text-sm">
        API by
        <a href="https://covid19api.com/" class="link" target="_blank">covid19api.com </a>•
      </p>

      <p class="text text-right text-sm">
        Desenvolvido por
        <a href="https://github.com/bloodstormm/" class="link" target="_blank">Nícolas Malachias </a>•
      </p>
      
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      isHidden: true,
    };
  },
  methods: {
    closeInfo() {
      this.isHidden = !this.isHidden;
    },
  },
};
</script>
