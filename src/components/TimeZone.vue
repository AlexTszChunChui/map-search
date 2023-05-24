<template>
    <base-card>
    <p>Recent Search Place: {{ recentSearch }} </p>
    <p>TimeZone: {{ timeZone }}</p>
    <p>Time: {{ currentTime }}</p>
    </base-card>
</template>

<script>
import axios from 'axios'
export default {
    props: ['searchHistory'],
    data() {
        return {
            timeZone: '',
            currentTime: '',
        }
    },
    computed: {
        recentSearch() {
            this.relativeTimeZone();
            return this.searchHistory[0].searchParams;
        },
    },
    methods: {
        async relativeTimeZone() {
            const latitude = this.searchHistory[0].coordinates[1];
            const longitude = this.searchHistory[0].coordinates[0];
            let zoneName;
            let currentTime;
            await axios.get(
                `http://api.timezonedb.com/v2.1/get-time-zone?key=CY0V5XP5G77Y&format=json&by=position&lat=${latitude}&lng=${longitude}`
                ).then((response) => {
                    zoneName = response.data.zoneName;
                    currentTime = response.data.formatted;
                });
            this.timeZone = zoneName;
            this.currentTime = currentTime;
        }
    },
};
</script>