<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import Score from './components/Score.vue';
import Button from './components/Button.vue';
import Card from './components/Card.vue';

const scoreCnt = ref(100);

const card = ref({
    word: "some word",
    translation: "Какое-то слово",
    state: "closed",
    status: "pending",
});

const onFlip = () => {
    card.value.state = "opened";
    console.log('Карта перевернулась');
}

const onStatusChange = () => {
    card.value.status = "success";
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
        <Card v-bind="card" @flip="onFlip" @statusChange="onStatusChange"></Card>
    </main>

</template>

<style scoped></style>