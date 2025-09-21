<script setup>
import { defineProps } from 'vue';

import HeartIcon from '../components/icons/HeartIcon.vue';

const { cnt = 0 } = defineProps({
    cnt: { type: Number, },
});

</script>

<template>
    <div class="score-wrap">
        <span>{{ cnt }}</span>
        <HeartIcon></HeartIcon>
    </div>
</template>

<style scoped>
.score-wrap {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: var(--color-blue-light);
    color: var(--color-blue);
    gap: 10px;
    font-size: 16px;
    padding: 12px 24px;
    border-radius: 36px;
}
</style>