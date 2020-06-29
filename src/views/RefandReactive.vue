<!--  -->
<template>
  <div></div>
</template>

<script>
import { ref, computed } from "vue";
export default {
  setup() {
    const count = ref(1);
    const plusOne = computed({
      get: () => count.value + 100,
      set: val => {
        count.value = val - 1;
      }
    });

    plusOne.value = 1;
    console.log(count.value); // 0
    console.log(plusOne.value); // 100
  }
};
</script>
<style lang='less' scoped>
</style>