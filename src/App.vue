<template>
    <main class="main">
        <ButtonView aria-label="Начать новую игру">Начать игру</ButtonView>
    </main>
</template>


<script setup>
import ButtonView from './components/ButtonView.vue';

</script>


<style scoped>
.main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100dvh;
}
</style>
