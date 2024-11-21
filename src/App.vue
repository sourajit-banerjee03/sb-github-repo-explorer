<template>
  <div id="app" class="container">
    <div class="input-group">
      <input v-model="username" placeholder="Enter GitHub Username" class="input" />
      <button @click="fetchRepos" class="button">Get Repos</button>
    </div>
    <RepoList 
      v-if="repositories.length" 
      :repositories="repositories" 
      @select="selectRepo" 
      :selectedRepo="selectedRepo" 
    />
    <div v-if="error" class="error">{{ error }}</div>
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
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.input-group {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

.button {
  padding: 10px 20px;
  font-size: 16px;
  color: #fff;
  background-color: #007bff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.button:hover {
  background-color: #0056b3;
}

.error {
  color: red;
  margin-top: 20px;
}
</style>