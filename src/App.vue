<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-lg-6">
          <div class="card border-secondary">
            <div class="card-header bg-primary">
              <h3>Choose username</h3>
            </div>
            <div class="card-body">
              <div class="row">
                <div class="col-12">
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
              </div>
            </div>
            <div class="card-footer">
              This is footer
            </div>
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
import $ from 'jquery';

export default {
  name: 'app',
  components: {
    HelloWorld,
    RepoList
  },
  data: () => ({
    username: 'octocat',
    repos: ['abc']
  }),
  beforeCreate() {
    console.log({...this})
  },
  created() {
    this.loadRepositories();
    console.log({...this})
  },
  mounted() {
    window.VueInstance = this;
    $('input').hide();
    $('input').fadeIn(2000);
  },
  updated() {
    console.log('Updated')
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

.box {
  margin: 2rem;
  background: orangered;
  border: yellow solid .4rem;
  padding: 45%;
}
</style>
