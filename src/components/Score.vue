<template>
    <div class="score">
        <div class="score-text">{{ points }}</div>
        <IconHeart class="score-icon" aria-hidden="true" />
    </div>
</template>

<script setup>
import { inject } from 'vue';
import IconHeart from './IconHeart.vue';
import { providePoints } from '@/constants';

const points = inject(providePoints);

</script>

<style scoped>
.score {
    display: flex;
    width: fit-content;
    align-items: center;
    gap: 10px;
    color: var(--color-like);
    background: var(--color-like-bg);
    padding: 12px 24px;
    border-radius: 36px;
}

.score-text {
    font-family: var(--font);
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;
}

.score-icon {
    width: 18px;
    height: 16px;
}
</style>