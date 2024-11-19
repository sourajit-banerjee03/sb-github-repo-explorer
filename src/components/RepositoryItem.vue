<template>
  <li @click="handleClick">
    {{ repo.name }} - ⭐ {{ repo.stargazers_count }}
  </li>
</template>

<script>
export default {
  props: ['repo'],
  methods: {
    handleClick() {
      this.$emit('select', this.repo);
    }
  }
};
</script>

<style scoped>
/* Add some basic styles */
</style>
