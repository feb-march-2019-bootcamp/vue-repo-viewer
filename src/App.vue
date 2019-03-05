<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-lg-6">
          <div class="form-group">
            <input type="text" 
              @keypress.enter="loadRepositories"
              class="form-control" v-model="username">
          </div>
          <div class="form-group">
            <button @click="loadRepositories" class="btn btn-primary btn-block">
              Load Repisitories
            </button>
          </div>
        </div>
        <div class="col-lg-6">
          <repo-list :repos="repos"></repo-list>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';

import HelloWorld from './components/HelloWorld.vue'
import RepoList from './components/RepoList.vue'
import Axios from 'axios'

export default {
  name: 'app',
  components: {
    HelloWorld,
    RepoList
  },
  data: () => ({
    username: 'octocat',
    repos: []
  }),
  mounted() {
    this.loadRepositories();
  },
  methods: {
    loadRepositories() {
      this.repos = [];
      
      Axios.get(`https://api.github.com/users/${this.username}/repos`)
        .then(res => {
          this.repos = res.data;
        }).catch(console.log);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
