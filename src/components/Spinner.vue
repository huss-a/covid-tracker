<template>
  <div class="spinner flex h-24 w-24 mb-10 justify-center relative">
    <div
      class="absolute border-transparent border-8 w-full h-full rounded-full"
    ></div>
    <div
      class="absolute border-transparent border-8 w-full h-full rounded-full"
    ></div>
  </div>
</template>

<script>
export default {
  props: ["spinnerColor"],
};
</script>

<style scoped>
.spinner div {
  border-top-color: #991b1b; /* equal to bg-red-800 */
  animation: spinnerOne .7s ease-out infinite;
}
.spinner div:nth-child(2) {
  border-bottom-color: #991b1b;
  animation: spinnerTwo .7s ease-out infinite;
}
@keyframes spinnerOne {
  0% {
    transform: rotate(0deg);
    border-width: 8px;
  }
  50% {
    transform: rotate(180deg);
    border-width: 2px;
  }
  100% {
    transform: rotate(360deg);
    border-width: 8px;
  }
}

@keyframes spinnerTwo {
  0% {
    transform: rotate(0deg);
    border-width: 2px;
  }
  50% {
    transform: rotate(180deg);
    border-width: 8px;
  }
  100% {
    transform: rotate(360deg);
    border-width: 2px;
  }
}
</style>
