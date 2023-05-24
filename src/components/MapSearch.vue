<template>
    <base-card>
        <form @submit.prevent="handleSubmit">
            <label>Please Enter a place </label>
            <input type="text" v-model="searchTerm">
            <base-button>Search</base-button>
            <base-button @click="shareLocation">Share Your Location</base-button>
        </form>
    </base-card>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            searchTerm: '',
        }
    },
    methods: {
        async handleSubmit() {
            let coordinates;
            await axios.get(`https://api.maptiler.com/geocoding/${this.searchTerm.trim()}.json?key=PS2Z0oN8xndXP36dLDUH`)
                .then((res) => {
                    coordinates = res.data.features[0].geometry.coordinates;
                });
            this.$emit('submit-search', coordinates, this.searchTerm);
            this.searchTerm = '';
        },
        shareLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition((position) => {
                    console.log(position.coords.latitude);
                    console.log(position.coords.longitude);
                },
                    (err) => {
                        alert(err.message);
                    }
                )
            } else {
                alert("Geolocation is not supported by your browser");
            }
        },
    },
};
</script>

<style>
</style>