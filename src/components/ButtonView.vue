<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script setup>

</script>

<style scoped>
.btn {
    background-color: var(--color-btn);
    width: 335px;
    padding: 10px 16px;
    border: none;
    border-radius: 100px;
    color: var(--color-secondery);
    font-size: 24px;
    line-height: 36px;
}

.btn:hover {
    background-color: var(--color-btn-hover);
}
</style>