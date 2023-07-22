<script setup>
    defineProps(["inicio", "fin", "maxLength"]);
    const emit = defineEmits(["next", "prev"]);
</script>

<template>
    <div class="btn-group">
        <button
            type="button"
            class="btn btn-primary"
            @click="emit('prev')"
            :disabled="inicio === 0">
            Anterior
        </button>
        <button
            type="button"
            class="btn btn-primary"
            @click="emit('next')"
            :disabled="fin >= maxLength">
            Siguiente
        </button>
    </div>
</template>