<script>
import { ref, watch } from 'vue';

export default {
    setup() {
        const timerLeft = ref(180)
        const selectedDifficulty = ref('Легкий')
        const difficulty = [
            'Легкий',
            'Средний',
            'Сложный',
            'Пользовательский'
        ]
        const selectCalculation = ref('Сложение/Вычитание')
        const Calculation = [
            'Сложение/Вычитание',
            'Умножение/Деление',
            'Микс'
        ]

        watch(selectedDifficulty, (newDiff) => {
            if (newDiff === 'Легкий') {
                timerLeft.value = 180;
                selectCalculation.value = 'Сложение/Вычитание';
            }
            else if (newDiff === 'Средний') {
                timerLeft.value = 120;
                selectCalculation.value = 'Умножение/Деление';
            }
            else if (newDiff === 'Сложный') {
                timerLeft.value = 60;
                selectCalculation.value = 'Микс';
            }
        })
        return {
            timerLeft,
            difficulty,
            selectedDifficulty,
            Calculation,
            selectCalculation
        }
    }
}
</script>

<template>
    <h2>Настройки</h2>
    <div>
        <p>Выбор сложности</p>
        <select v-model="selectedDifficulty">
            <option v-for="difficultyLevel in difficulty" :key="difficultyLevel" :value="difficultyLevel">{{ difficultyLevel }}</option>
        </select>
    </div>
    

    <div>
        <p>Выбор таймера</p>
        <select :disabled="selectedDifficulty !== 'Пользовательский'" v-model="timerLeft">
            <option value="60">60 секунд</option>
            <option value="120">120 секунд</option>
            <option value="180">180 секунд</option>
        </select>
    </div>

    <div>
        <p>Выбор операций</p>
        <select :disabled="selectedDifficulty !== 'Пользовательский'" v-model="selectCalculation">
            <option v-for="difficalc in Calculation" :key="difficalc" :value="difficalc">{{ difficalc }}</option>
        </select>
    </div>
    
</template>

<style scoped>
select {
    margin-bottom: 10px;
    padding: 5px;
    border-radius: 5px;
    width: 100%;
    background-color: #f1f1f1;
    color: #333;
    border: none;
}

p {
    margin-bottom: 10px;
    font-weight: bold;
    font-size: 18px;
    color: #333;
    text-align: center;
}
</style>