<template>
    <ul>
        <base-card>
        <p>Searching History</p>
        <base-button @click="handleDelete">Delete</base-button>
        <search-history
        v-for="search in slicedHistory"
        :key="search.id"
        :params="search.searchParams"
        :id="search.id"
        ></search-history>
        <base-button v-if="page > 0" @click="goPrevPage">Prev Page</base-button>
        <base-button v-if="searchHistory.length > page + 10" @click="goNextPage">Next Page</base-button>
    </base-card>
    </ul>
</template>

<script>
import SearchHistory from './SearchHistory.vue';
export default {
    data() {
        return {
            page: 0,
        }
    },
    components: {
        SearchHistory,
    },
    computed: {
        slicedHistory() {
            return this.searchHistory.slice(this.page, this.page + 10);
        },
    },
    props: ['searchHistory'],
    methods: {
        handleDelete() {
            this.$emit('submit-delete');
            this.page = 0;
        },
        goNextPage() {
            this.page += 10;
        },
        goPrevPage() {
            this.page -= 10;
        }
    }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>