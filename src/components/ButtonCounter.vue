<script setup>
    import { ref } from 'vue';
    const counter = ref(0);
    const increment = () => counter.value++;
</script>

<template>
    <div class="container">
        <button @click="increment">Counter: {{counter}}</button>
    </div>
</template>

<style>
</style>