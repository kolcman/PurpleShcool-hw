<template>
    <Header />
    <main class="main">
        <!-- <Button aria-label="Начать новую игру">Начать игру</Button> -->
        <ul class="card-list">
            <Card v-for="card in data" :key="card.num" v-bind="card" @flip-card="flipCard" />
        </ul>
    </main>
</template>


<script setup>
// import Button from '@/components/Button.vue';
import Header from '@/components/Header.vue';
import Card from '@/components/Card.vue'
import { ref } from 'vue';


const data = ref([
    {
        num: "01",
        word: "Apple",
        translation: "Яблоко",
        state: false,
        status: "pending"
    },
    {
        num: "02",
        word: "Green",
        translation: "Зеленый",
        state: true,
        status: "pending"
    },
    {
        num: "03",
        word: "Army",
        translation: "Армия",
        state: true,
        status: "right"
    },
    {
        num: "04",
        word: "Car",
        translation: "Автомобиль",
        state: true,
        status: "wrong"
    },

])


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

.card-list {
    display: flex;
    flex-wrap: wrap;
    gap: 66px 107px;
}
</style>
