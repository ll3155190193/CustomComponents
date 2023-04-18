<template>
  <MButton @click="handleClick">Click me</MButton>
</template>
<script>
import MButton from './components/MButton.vue';
export default {
  components: {
    MButton
  },
  methods: {
    async handleClick() {
      // do something async
      await new Promise((resolve, reject) => {
          setTimeout(() => {
            resolve(console.log(666))
          }, 2000);
      })
    }
  }
};
</script>
<style>
</style>
