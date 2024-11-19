<template>
  <div>
    <h2>Repositories</h2>
    <ul>
      <RepoItem 
        v-for="repo in repositories" 
        :key="repo.id" 
        :repo="repo" 
        @select="selectRepo" 
      />
    </ul>
    <RepoDetails v-if="selectedRepo" :repo="selectedRepo" />
  </div>
</template>

<script>
import RepoItem from './RepositoryItem.vue';
import RepoDetails from './RepositoryDetails.vue';

export default {
  components: { RepoItem, RepoDetails },
  props: ['repositories', 'selectRepo', 'selectedRepo']
};
</script>

<style scoped>
/* Add some basic styles */
</style>
