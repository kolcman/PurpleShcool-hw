<template>
    <div class="header">
        <h1 class="header-title">Запомни слово</h1>
        <Score class="header-count" :count="100" />
    </div>
</template>

<script setup>
import Score from '@/components/Score.vue'
</script>

<style scoped>
.header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 37px 62px;
}

.header-title {
    font-family: var(--font);
    font-weight: 700;
    font-size: 16px;
    text-transform: uppercase;
    color: var(--color-text);

}

.header-count {}
</style>