<template>
  <div
    id="app"
    class="d-flex justify-content-center align-items-center vh-100 bg-light"
  >
    <Calculator />
  </div>
</template>

<script>
import Calculator from "./components/SimpleCalculator.vue";

export default {
  components: {
    Calculator,
  },
};
</script>
