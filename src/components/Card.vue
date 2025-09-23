<script setup>
import { defineEmits } from 'vue';
import SuccessIcon from '../components/icons/SuccessIcon.vue';
import FailIcon from '../components/icons/FailIcon.vue';

const props = defineProps(['id', 'word', 'translation', 'state', 'status']);

const emit = defineEmits(['flip', 'statusChange'])

function handleFlip() {
    emit('flip', true);
}

function changeStatus() {
    emit('statusChange', true)
}

</script>

<template>
    <div class="card">
        <div class="card-header">
            <span>{{ props.id }}</span>
            <SuccessIcon v-if="props.status === 'success'" />
            <FailIcon v-if="props.status === 'fail'" />
        </div>
        <div class=" card-content">
            <span>{{ props.word }}</span>
        </div>
        <div class="card-footer">
            <span v-if="props.state === 'closed' && props.status === 'pending'" @click="handleFlip">
                Перевернуть
            </span>

            <span v-if="props.state === 'opened' && props.status === 'pending'">
                <SuccessIcon @click="changeStatus" />
                <FailIcon @click="changeStatus" />
            </span>

            <span v-if="props.status === 'success' || props.status === 'fail'">
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