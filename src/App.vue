<template>
    <Header class="header" />
    <main class="main">
<<<<<<< Updated upstream
        <!-- <Button aria-label="Начать новую игру">Начать игру</Button> -->
        <ul class="card-list">
            <Card v-for="card in data" :key="card.num" v-bind="card" @flip-card="flipCard(card)"
                @change-status="(newStatus) => changeStatus(card, newStatus)" />
        </ul>
=======
        <Button v-if="!isGameStarted" class="btn btn-start" aria-label="Начать новую игру" @click="startGame()">Начать
            игру</Button>
        <div v-else class="game">
            <ul class="card-list">
                <Card v-for="card in data" :key="card.id" v-bind="card" @flip-card="flipCard(card)"
                    @change-status="(newStatus) => changeStatus(card, newStatus)" />
            </ul>
            <Button class="btn btn-restart" aria-label="Начать заново" @click="restartGame()">Заново</Button>
        </div>
>>>>>>> Stashed changes
    </main>
</template>


<script setup>
// import Button from '@/components/Button.vue';
import Header from '@/components/Header.vue';
import Card from '@/components/Card.vue'
<<<<<<< Updated upstream
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
]);
=======
import { onMounted, provide, ref } from 'vue';
import { API_ENDPOINT, providePoints } from '@/constants';

onMounted(() => {
    loadData()
})


const data = ref();
const points = ref(0);
let isGameStarted = ref(false);

provide(providePoints, points)

async function loadData() {
    const res = await fetch(API_ENDPOINT);
    if (res.ok) {
        const raw = await res.json()

        data.value = raw.map((word, index) => ({
            id: index,
            word: word.word,
            translation: word.translation,
            state: false,
            status: 'pending',
        }));
    }
}
>>>>>>> Stashed changes

function startGame() {
    return isGameStarted.value = true
}

function restartGame() {
    loadData()
    points.value = 0
}

function flipCard(card) {
    card.state = true
}

function changeStatus(card, newStatus) {
    card.status = newStatus
}


</script>

<style scoped>
.header {
    margin-bottom: 50px;
}

.main {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100dvh;
}

.game {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

}

.card-list {
    display: flex;
    flex-wrap: wrap;
    gap: 66px 107px;
    margin-bottom: 100px;
}


.btn {
    background-color: var(--color-btn);
    min-width: 335px;
    width: max-content;
    padding: 10px 16px;
    border: none;
    border-radius: 100px;
    color: var(--color-secondary);
    font-size: 24px;
    line-height: 36px;
}

.btn:hover {
    background-color: var(--color-btn-hover);
}
</style>
