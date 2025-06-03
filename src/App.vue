<template>
    <Header class="header" />
    <main class="main">
        <ErrorMessage v-if="error" class="error" />
        <Button v-if="!isGameStarted" class="btn btn-start" aria-label="Начать новую игру" @click="startGame()">Начать
            игру</Button>
        <div v-else class="game">
            <ul class="card-list">
                <Card v-for="card in data" :key="card.id" v-bind="card" @flip-card="flipCard(card)"
                    @change-status="(newStatus) => changeStatus(card, newStatus)" />
            </ul>
            <Button class="btn btn-restart" aria-label="Начать заново" @click="restartGame()">Заново</Button>
        </div>
    </main>
</template>


<script setup>
import Header from '@/components/Header.vue';
import Card from '@/components/Card.vue'
import { onMounted, provide, ref } from 'vue';
import { API_ENDPOINT, providePoints } from '@/constants';
import ErrorMessage from './components/ErrorMessage.vue';

onMounted(() => {
    loadData()
})


const data = ref();
const points = ref(0);
let isGameStarted = ref(false);
let error = ref(false)

provide(providePoints, points)

async function loadData() {
    try {
        const res = await fetch(API_ENDPOINT);
        if (!res.ok) {
            throw new Error('Ошибка загрузки данных');
        }

        const raw = await res.json();

        data.value = raw.map((word, index) => ({
            id: index,
            word: word.word,
            translation: word.translation,
            state: false,
            status: 'pending',
        }));

        error.value = false;
    } catch (err) {
        error.value = true;
    }
}

function startGame() {
    return isGameStarted.value = true
}

function restartGame() {
    isGameStarted.value = false;
    error.value = false
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
    flex-direction: column;
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


.error {
    margin: 0 auto;
    font-size: 52px;
    color: red;
}
</style>
