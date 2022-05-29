<template>
  <div>
    <h1>Vue</h1>
  </div>
</template>

<script>
import { onMounted } from "vue";

// Composition API
export default {
  setup() {
    onMounted(() => {
      console.log("foi montado composition api");
    });
  },
};
// Options API
// export default {
//   mounted() {
//     console.log("foi montado Options API");
//   },
// };
</script>