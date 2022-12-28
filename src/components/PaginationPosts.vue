<script setup>
defineProps(["start", "end", "maxPosts"]);
const emit = defineEmits(["nextPage", "prevPage"]);
</script>

<template>
    <div
        class="vb-pagination btn-group"
        role="group"
        aria-label="Basic example"
    >
        <button
            type="button"
            class="vb-pagination__btn vb-pagination__btn--prev btn btn-secondary"
            @click="emit('prevPage')"
            :disabled="start <= 0"
        >
            Anterior
        </button>
        <button
            type="button"
            class="vb-pagination__btn vb-pagination__btn--next btn btn-secondary"
            @click="emit('nextPage')"
            :disabled="end >= maxPosts"
        >
            Siguiente
        </button>
    </div>
</template>
