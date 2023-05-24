<template>
    <li>
        <base-card>
        <input type="checkbox" @click="handleClick">
        <p>{{ params }}</p>
        </base-card>
    </li>
</template>

<script>
export default {
    inject: ['toggleDelete'],
    props: ['params', 'id'],
    methods: {
        handleClick() {
            this.toggleDelete(this.id);
        },
    },
}
</script>

<style scoped>
li {
    margin: auto;
    max-width: 40rem;
}
input {
    display: flex;
    justify-content: space-between;
    align-items: left;
}
p {
    margin: 0.5rem 0;
}
</style>