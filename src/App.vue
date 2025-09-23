<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import Score from './components/Score.vue';
import Button from './components/Button.vue';
import Card from './components/Card.vue';

const scoreCnt = ref(100);

const cards = ref([
    {
        id: 1,
        word: "A table",
        translation: "Стол",
        state: "closed",
        status: "pending",
    },
    {
        id: 2,
        word: "A cat",
        translation: "Кошка",
        state: "opened",
        status: "pending",
    },
    {
        id: 3,
        word: "A car",
        translation: "Машина",
        state: "opened",
        status: "success",
    },
    {
        id: 4,
        word: "A pen",
        translation: "Ручка",
        state: "opened",
        status: "fail",
    }
]);

const onFlip = () => {
    //card.value.state = "opened";
    console.log('Карта перевернулась');
}

const onStatusChange = () => {
    //card.value.status = "success";
    console.log('Статус изменен');
}
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