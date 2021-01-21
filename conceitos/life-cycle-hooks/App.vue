<template>
  <h1>Lifecycle Hooks</h1>
</template>

<script>
import { onMounted } from "vue";
export default {
  setup() {
    onMounted(() => {
      console.log("Foi montado compostion");
    });
  },
};
// export default {
//     mounted() {
//         console.log('Foi montado options API');
//     }
// }
</script>

<style>
</style>