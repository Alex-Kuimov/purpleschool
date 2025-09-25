<script setup>
import { ref, computed, watch } from 'vue';
import Header from './components/Header.vue';
import Score from './components/Score.vue';
import Button from './components/Button.vue';
import Card from './components/Card.vue';

const scoreCnt = ref(0);
const cards = ref([]);
const loading = ref(false);
const error = ref(null);
const gameStarted = ref(false);
const gameOver = ref(false);

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

const startGame = () => {
    gameStarted.value = true;
    gameOver.value = false;
    scoreCnt.value = 0;
    fetchCards();
}

const restartGame = () => {
    gameStarted.value = true;
    gameOver.value = false;
    scoreCnt.value = 0;
    cards.value = [];
    fetchCards();
}

const onFlip = (card) => {
    const cardIndex = cards.value.findIndex(c => c.id === card.id);

    if (cardIndex !== -1) {
        cards.value[cardIndex].state = cards.value[cardIndex].state === 'closed' ? 'opened' : 'closed';
    }
}

const onStatusChange = (card, status) => {
    const cardIndex = cards.value.findIndex(c => c.id === card.id);

    if (cardIndex !== -1) {
        cards.value[cardIndex].status = status;
        
        if (status === 'success') {
            scoreCnt.value += 10;
        } else if (status === 'fail') {
            scoreCnt.value -= 4;
        }
    }
}

// Отслеживаем изменение статуса карт
watch(cards, (newCards) => {
    if (newCards.length === 10 && newCards.every(card => 
        card.status === 'success' || card.status === 'fail'
    )) {
        gameOver.value = true;
    }
}, { deep: true });
</script>

<template>
    <Header>
        <h1>ЗАПОМНИ СЛОВО</h1>
        <Score :cnt="scoreCnt"></Score>
    </Header>

    <main>
        <div class="cards-list">
            <Card v-for="card in cards" :key="card.id" v-bind="card" @flip="onFlip" @statusChange="onStatusChange">
            </Card>
        </div>
        
        <Button v-if="!gameStarted" @click="startGame">Начать игру</Button>
        <Button v-if="gameOver" @click="restartGame">Начать заново</Button>
    </main>
</template>

<style scoped>
.cards-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin: 40px 0;
    gap: 20px;
}
</style>