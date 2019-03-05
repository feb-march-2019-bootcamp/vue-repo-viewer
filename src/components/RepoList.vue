<template>
    <ul class="list-group">
        <li v-for="(repo, i) in repos"
            class="list-group-item"
            :class="{[liClasses[i % liClasses.length]]: true}"
            :key="repo.id">
            <a v-bind:href="repo.html_url" v-text="repo.name"></a>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'repo-list',
    props: {
        repos: {default: () => [], type: Array}
    },
    data: () => ({
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
    })
}
</script>

<style scoped>
     
</style>

