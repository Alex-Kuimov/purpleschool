<script setup>
import { defineEmits } from 'vue';
import SuccessIcon from '../components/icons/SuccessIcon.vue';
import FailIcon from '../components/icons/FailIcon.vue';

const card = defineProps(['id', 'word', 'translation', 'state', 'status']);

const emit = defineEmits(['flip', 'statusChange'])

function handleFlip() {
    emit('flip', card);
}

function changeStatus(status) {
    emit('statusChange', card, status)
}

</script>

<template>
    <div class="card">
        <div class="card-header">
            <span>{{ card.id }}</span>
            <SuccessIcon v-if="card.status === 'success'" />
            <FailIcon v-if="card.status === 'fail'" />
        </div>
        <div class=" card-content">
            <span>{{ card.word }}</span>
        </div>
        <div class="card-footer">
            <span v-if="card.state === 'closed' && card.status === 'pending'" @click="handleFlip">
                Перевернуть
            </span>

            <span v-if="card.state === 'opened' && card.status === 'pending'">
                <SuccessIcon @click="changeStatus('success')" />
                <FailIcon @click="changeStatus('fail')" />
            </span>

            <span v-if="card.status === 'success' || card.status === 'fail'">
                Завершено
            </span>
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