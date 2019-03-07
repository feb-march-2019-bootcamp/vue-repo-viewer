<template>
    <!-- <ul class="list-group">
        <li v-for="(repo, i) in repos"
            class="list-group-item"
            :class="{[liClasses[i % liClasses.length]]: true}"
            :key="repo.id">
            <a v-bind:href="repo.html_url" v-text="repo.name"></a>
        </li>
    </ul> -->
    <div class="table-responsive">
        <table class="table table-bordered table-striped table-hover">
            <thead class="table-dark">
                <tr>
                    <th>Id</th>
                    <th>Name</th>
                    <th>Thumbnail</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="repo in repos" :key="repo.id">
                    <td v-text="repo.id"></td>
                    <td v-text="repo.name"></td>
                    <td>
                        <div style="width: 3rem">
                            <img class="img-fluid img-thumbnail rounded" :src="repo.owner.avatar_url" alt="">
                        </div>
                    </td>
                    <th>
                        <div class="btn-group">
                            <a class="btn btn-info" 
                            :href="repo.html_url">Visit</a>
                            <button class="btn btn-danger" @click="deleteRepo(repo)">Delete</button>
                        </div>
                    </th>
                </tr>
            </tbody>
        </table>

        <!-- <b-table :items="repos" :fields="fields ">

        </b-table> -->

        <b-modal title="Pay Attention"
         header-bg-variant="danger" 
         header-text-variant="light"
         v-model="showDeleteModal" @ok="$emit('delete-repo', repoId)">
            Are you sure to delete?
        </b-modal>
    </div>
</template>

<script>
export default {
    name: 'repo-list',
    props: {
        repos: {default: () => [], type: Array}
    },
    data: () => ({
        repoId: null,
        showDeleteModal: false,
        fields: [
            'id',
            'name',

        ],
        liClasses: [
            '',
            'list-group-item-primary',
            'list-group-item-secondary',
            'list-group-item-success',
            'list-group-item-danger',
            'list-group-item-warning',
            'list-group-item-info',
            'list-group-item-light',
            'list-group-item-dark'
        ]
    }),
    methods: {
        deleteRepo(repo) {
            this.repoId = repo.id;
            this.showDeleteModal = true;
        }
    }
}
</script>

<style scoped>
     
</style>

