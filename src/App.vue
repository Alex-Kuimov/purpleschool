<script setup>
import Header from './components/Header.vue';
import Score from './components/Score.vue';
import Button from './components/Button.vue';
import Card from './components/Card.vue';


const onFlip = () => {
    console.log('Карта перевернулась')
}

const onStatusChange = () => {
    console.log('Статус изменен')
}

</script>

<template>
    <Header>
        <h1>ЗАПОМНИ СЛОВО</h1>
        <Score cnt="100"></Score>
    </Header>

    <main>
        <Button>Начать игру</Button>

        <Card @flip="onFlip" @statusChange="onStatusChange"></Card>
    </main>

</template>

<style scoped></style>