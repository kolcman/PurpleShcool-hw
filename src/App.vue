<template>
    <Header />
    <main class="main">
        <!-- <Button aria-label="Начать новую игру">Начать игру</Button> -->
        <Card v-bind="card" @flip-card="flipCard" />
    </main>
</template>


<script setup>
// import Button from '@/components/Button.vue';
import Header from '@/components/Header.vue';
import Card from '@/components/Card.vue'
import { ref } from 'vue';

const card = ref({
    num: "01",
    word: "word",
    translation: "transl",
    state: "open",
    status: "pending"
})

function flipCard() {

}

</script>


<style scoped>
.main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100dvh;
}
</style>
