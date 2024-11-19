<template>
  <div id="app">
    <input v-model="username" placeholder="Enter GitHub Username" />
    <button @click="fetchRepos">Get Repos</button>
    <RepoList 
      v-if="repositories.length" 
      :repositories="repositories" 
      @select="selectRepo" 
      :selectedRepo="selectedRepo" 
    />
    <div v-if="error">{{ error }}</div>
  </div>
</template>

<script>
import RepoList from './components/RepositoryList.vue';
import axios from 'axios';

export default {
  components: { RepoList },
  data() {
    return {
      username: '',
      repositories: [],
      selectedRepo: null,
      error: ''
    };
  },
  methods: {
    async fetchRepos() {
      this.error = '';
      try {
        const response = await axios.get(`https://api.github.com/users/${this.username}/repos`);
        this.repositories = response.data;
      } catch (err) {
        this.error = 'User not found or API error.';
      }
    },
    selectRepo(repo) {
      this.selectedRepo = repo;
    }
  }
};
</script>

<style>
/* Add some basic styles */
</style>