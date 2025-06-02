<template>
    <div class="card">
        <div class="card-inner">
            <div class="card-number">{{ props.num }}</div>
            <div class="card-words">
                <div v-if="!state">{{ props.word }}</div>
                <div v-else>{{ props.translation }}</div>
            </div>
            <div class="card-btns">

                <button v-if="state && status === 'pending'" class="btns-wrong" @click="changeStatus('wrong')">
                    <IconWrong />
                </button>
                <button v-if="state && status === 'pending'" class="btns-right" @click="changeStatus('right')">
                    <IconRight />
                </button>

                <button v-else-if="!state" class="btns-flip" @click="flipCard()">
                    Перевернуть
                </button>
                <div v-else class="card-status">Завершено</div>
            </div>
            <div>
                <IconRight v-if="status === 'right'" class="card-icon" />
                <IconWrong v-else-if="status === 'wrong'" class="card-icon" />
            </div>
        </div>
    </div>
</template>

<script setup>

import { inject } from 'vue';
import IconRight from './IconRight.vue'
import IconWrong from './IconWrong.vue'
import { providePoints } from '@/constants';

const points = inject(providePoints);
const props = defineProps({
    num: String,
    word: String,
    translation: String,
    state: Boolean,
    status: String
});
const emit = defineEmits(['flipCard', 'changeStatus'])


function changeStatus(newStatus) {
    if (newStatus === 'wrong') {
        if (points.value >= 4) {
            points.value -= 4
            console.log(points);
        }
    }
    else if (newStatus === "right") {
        points.value += 10
    }
    emit('changeStatus', newStatus)
}

function flipCard() {
    emit('flipCard')
}
</script>


<style scoped>
.card {
    width: 250px;
    height: 376px;
    background: var(--color-secondary);
    border-radius: 16px;
    box-shadow: 0px 0px 16px 0px #0000001A;
    padding: 28px 19px;
    position: relative;
}

.card:hover {
    box-shadow: 10px 10px 10px 0px #0000000D;
}

.card-inner {
    border: 1px solid var(--color-card-border);
    height: 100%;
    border-radius: 12px;
    display: flex;
    justify-content: center;
    align-items: center;

}

.card-number {
    font-size: 14px;
    position: absolute;
    top: 28px;
    left: 35px;
    transform: translateY(-50%);
    background: var(--color-secondary);
}


.card-words {
    font-size: 18px;
    line-height: 100%;
    text-transform: lowercase;

}

.card-btns {
    display: flex;
    gap: 32px;
    padding: 9px;
    background: var(--color-secondary);
    justify-content: space-between;
    position: absolute;
    bottom: 28px;
    left: 50%;
    transform: translate(-50%, 50%);
}

.card-icon {
    position: absolute;
    width: 39px;
    height: 39px;
    top: 28px;
    left: 50%;
    transform: translate(-50%, -50%);

}


.btns-flip {
    border: none;
    background: var(--color-secondary);
    padding: 0 4px;
    width: fit-content;
    color: var(--color-text);
    font-weight: 700;
    font-size: 12px;
    line-height: 18px;
    text-transform: uppercase;
    cursor: pointer;
}

.btns-wrong,
.btns-right {
    width: fit-content;
    border: none;
    background: var(--color-secondary);
    cursor: pointer;
    justify-content: center;
    align-items: center;
}

.card-status {
    font-family: var(--font);
    font-weight: 700;
    font-size: 12px;
    line-height: 18px;
    letter-spacing: 12%;
    text-transform: uppercase;
}
</style>
