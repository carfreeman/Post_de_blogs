<script setup>
    import { ref } from "vue";
    const count = ref(0);
</script>

<template>
    <button @click="count++" class="btn btn-warning">You clicked me {{ count }} times</button>
</template>