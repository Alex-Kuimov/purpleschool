<script setup>
import { defineEmits } from 'vue'

const emit = defineEmits(['flip', 'statusChange'])

function handleFlip() {
    emit('flip', true);
}

function changeStatus() {
    emit('statusChange', true)
}

</script>

<template>
    <div class="card" @click="handleFlip">
        <div class="card-header">
            <span>01</span>
        </div>
        <div class="card-content">
            <span>Some word</span>
        </div>
        <div class="card-footer">
            <span @click.stop="changeStatus">Перевернуть</span>
        </div>
    </div>
</template>

<style scoped>
.card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 40px 30px;
    width: 250px;
    height: 376px;
    box-shadow: 0px 0px 16px 0px #0000001A;
    border-radius: 16px;
    cursor: pointer;
}

.card-content {
    display: flex;
    justify-content: center;
}

.card-footer {
    display: flex;
    justify-content: center;
}
</style>