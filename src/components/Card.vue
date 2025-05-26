<template>
    <div class="card">
        <div class="card-inner">
            <div class="card-number">{{ props.num }}</div>
            <div class="card-text">{{ props.word }}</div>
            <div class="card-text">{{ props.translation }}</div>
            <div class="btns">
                <button class="btns-flip" @click="flipCard()">Перевернуть</button>
                <button class="btns-wrong">
                    <IconWrong />
                </button>
                <button class="btns-right">
                    <IconRight />
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>

import IconRight from './IconRight.vue'
import IconWrong from './IconWrong.vue'

const props = defineProps({
    num: String,
    word: String,
    translation: String,
    state: String,
    status: String
});

const emit = defineEmits(['flipCard', 'changeStatus'])

function changeStatus() {
    emit('changeStatus')
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


.card-text {
    font-size: 18px;
    line-height: 100%;
    text-transform: lowercase;

}

.btns {
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


.btns-flip {
    border: none;
    background: var(--color-secondary);
    padding: 0 4px;
    width: fit-content;
    color: var(--color-text);
    font-weight: 700;
    font-size: 12px;
    line-height: 18px;
    letter-spacing: 12%;
    text-transform: uppercase;
    cursor: pointer;
}

.btns-wrong,
.btns-right {
    display: none;
    width: fit-content;
    border: none;
    background: var(--color-secondary);
    cursor: pointer;
    justify-content: center;
    align-items: center;
}


.visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    margin: -1px;
    border: 0;
    padding: 0;
    white-space: nowrap;
    clip-path: inset(100%);
    clip: rect(0 0 0 0);
    overflow: hidden;
}
</style>
