<template>
  <div id="app">
    <div class="row">
      <div class="container-fluid">
      <b-navbar toggleable="lg" type="dark" variant="dark">
        <b-navbar-brand href="#">NavBar</b-navbar-brand>

        <b-navbar-toggle target="nav_collapse"/>

        <b-collapse is-nav id="nav_collapse">
          <b-navbar-nav>
            <b-nav-item href="#">Link</b-nav-item>
            <b-nav-item href="#" disabled>Disabled</b-nav-item>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-form>
              <b-form-input size="sm" class="mr-sm-2" type="text" placeholder="Search"/>
              <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
            </b-nav-form>

            <b-nav-item-dropdown text="Lang" right>
              <b-dropdown-item href="#">EN</b-dropdown-item>
              <b-dropdown-item href="#">ES</b-dropdown-item>
              <b-dropdown-item href="#">RU</b-dropdown-item>
              <b-dropdown-item href="#">FA</b-dropdown-item>
            </b-nav-item-dropdown>

            <b-nav-item-dropdown right>
              <!-- Using button-content slot -->
              <template slot="button-content">
                <em>User</em>
              </template>
              <b-dropdown-item href="#">Profile</b-dropdown-item>
              <b-dropdown-item href="#">Signout</b-dropdown-item>
            </b-nav-item-dropdown>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>
    </div>
    <div class="container">
      <div class="row">
        <div class="col-lg-6">
          <!-- <div class="card border-secondary">
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
                    <b-button @click="loadRepositories" block variant="primary">
                      Load Repository
                    </b-button>
                  </div>
                </div>
              </div>
            </div>
            <div class="card-footer">
              This is footer
            </div>
          </div>-->
          <b-card header="Username">
            <b-card-body>
              <div class="row">
                <div class="col-12">
                  <div class="form-group">
                    <b-form-input
                      v-model="username"
                      @keypress.enter="loadRepositories"
                      placeholder="Enter email"
                    />
                  </div>
                  <div class="form-group">
                    <b-button @click="loadRepositories" block variant="primary">Load Repository</b-button>
                  </div>
                  <div class="form-group">
                    <b-form-file></b-form-file>
                  </div>
          
                </div>
              </div>
            </b-card-body>
          </b-card>
        </div>
        <div class="col-lg-6">
          <repo-list @delete-repo="handleDeleteRepo" :repos="repos"></repo-list>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import RepoList from './components/RepoList.vue'
import Axios from 'axios'
import $ from 'jquery'

export default {
  name: 'app',
  components: {
    HelloWorld,
    RepoList,
  },
  data: () => ({
    username: 'octocat',
    repos: ['abc'],
  }),
  beforeCreate() {
    console.log({ ...this })
  },
  created() {
    this.loadRepositories()
    console.log({ ...this })
  },
  mounted() {
    window.VueInstance = this
    $('input').hide()
    $('input').fadeIn(2000)
  },
  updated() {
    console.log('Updated')
  },
  methods: {
    loadRepositories() {
      this.repos = []

      Axios.get(`https://api.github.com/users/${this.username}/repos`)
        .then(res => {
          this.repos = res.data
        })
        .catch(console.log)
    },
    handleDeleteRepo(repoId) {
      this.repos = this.repos.filter(x => x.id !== repoId)
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.box {
  margin: 2rem;
  background: orangered;
  border: yellow solid 0.4rem;
  padding: 45%;
}
</style>
