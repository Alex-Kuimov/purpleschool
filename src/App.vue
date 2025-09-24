<script setup>
import { onMounted, ref } from 'vue';
import Header from './components/Header.vue';
import Score from './components/Score.vue';
import Button from './components/Button.vue';
import Card from './components/Card.vue';

const scoreCnt = ref(100);
const cards = ref([]);
const loading = ref(false);
const error = ref(null);

const fetchCards = async () => {
    loading.value = true;
    error.value = null;

    try {
        const response = await fetch('http://localhost:8080/api/random-words');

        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }

        const data = await response.json();

        cards.value = data.map((item, index) => ({
            id: index + 1,
            word: item.word,
            translation: item.translation,
            state: "closed",
            status: "pending",
        }));

    } catch (err) {
        error.value = err.message;
        console.error('Failed to fetch cards:', err);
    } finally {
        loading.value = false;
    }
};

const onFlip = () => {
    console.log('Карта перевернулась');
}

const onStatusChange = () => {
    console.log('Статус изменен');
}

onMounted(() => {
    fetchCards();
});
</script>

<template>
    <Header>
        <h1>ЗАПОМНИ СЛОВО</h1>
        <Score :cnt="scoreCnt"></Score>
    </Header>

    <main>
        <Button>Начать игру</Button>
        <Card v-for="card in cards" :key="card.id" v-bind="card" @flip="onFlip" @statusChange="onStatusChange"></Card>
    </main>
</template>

<style scoped></style>