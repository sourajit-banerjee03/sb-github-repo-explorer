<template>
  <div v-if="repo">
    <h3>Description</h3>
    <p>{{ repo.description || 'No description available' }}</p>
  </div>
</template>

<script>
export default {
  props: ['repo']
};
</script>

<style scoped>
/* Add some basic styles */
</style>
