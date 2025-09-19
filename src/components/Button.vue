<script setup>
</script>

<template>
    <button type="button" class="button">
        <slot></slot>
    </button>
</template>

<style scoped>
.button {
    background: var(--color-blue);
    color: var(--color-white);
    border: none;
    font-size: 24px;
    padding: 16px 10px;
    height: 68px;
    width: 335px;
    border-radius: 100px;
    cursor: pointer;
}
</style>