<script setup>
    defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Sin descripcion'
        },
        Favorite: Function,
    });

    const emit = defineEmits(["setFavorite"]);
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{ title }}</h5>
            <p>{{ body }}</p>
            <button
                class="btn btn-sm btn-warning"
                @click="emit('setFavorite', title)">
                Mi favorito
            </button>
        </div>
    </div>
</template>