<script setup>
defineProps(["title", "id", "body"]);
const emit = defineEmits(["addFavorite"]);
</script>

<template>
    <div class="vb-card col-sm-6 mb-4" :class="`vb-card--${id}`">
        <div class="vb-card-wrapp rounded p-4">
            <h2 class="vb-card-title h5">{{ id }} - {{ title }}</h2>
            <p class="vb-card-excerpt">{{ body }}</p>
            <button
                class="btn btn-outline-primary"
                @click="emit('addFavorite', title)"
            >
                Agregar a favoritos
            </button>
        </div>
    </div>
</template>
