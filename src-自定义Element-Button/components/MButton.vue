<template>
  <el-button v-bind="$attrs" :loading="isLoading" @click="handleClick" ref="button">
    <template v-if="!isLoading">
      <slot></slot>
    </template>
    <template v-else>
      <i class="el-icon-loading"></i>
    </template>
  </el-button>
</template>
<script>
export default {
  props: {
    debounceTime: {
      type: Number,
      default: 300
    }
  },
  data() {
    return {
      isLoading: false
    };
  },
  methods: {
    handleClick() {
      this.$emit("click");
    },
    async handleClickWithDebounce() {
      if (this.isLoading) return;
      this.isLoading = true;
      try {
        await this.$listeners.click();
      } catch (error) {
      } finally {
        this.isLoading = false;
      }
    }
  },
  created() {
    this.handleClick = _.debounce(this.handleClickWithDebounce, this.debounceTime);
  }
};
</script>