<template>
    <Header />
    <main class="main">
        <!-- <Button aria-label="Начать новую игру">Начать игру</Button> -->
        <ul class="card-list">
            <Card v-for="card in data" :key="card.id" v-bind="card" @flip-card="flipCard(card)"
                @change-status="(newStatus) => changeStatus(card, newStatus)" />
        </ul>
    </main>
</template>


<script setup>
// import Button from '@/components/Button.vue';
import Header from '@/components/Header.vue';
import Card from '@/components/Card.vue'
import { onMounted, ref } from 'vue';

onMounted(() => {
    loadData()
})

const API_ENDPOINT = 'http://localhost:8080/api/random-words';


const data = ref();

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


function flipCard(card) {
    card.state = true
}

function changeStatus(card, newStatus) {
    card.status = newStatus
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
