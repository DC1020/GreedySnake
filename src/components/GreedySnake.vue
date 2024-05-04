<template>
    <div id="app">
        <div id="game-board">
            <div v-for="(row, rowIndex) in gameBoard" :key="rowIndex">
                <div v-for="(cell, colIndex) in row" :key="colIndex" :class="getCellClass(rowIndex, colIndex)"></div>
            </div>
        </div>
        <button @click="startGame">Start Game</button>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const gameBoard = ref([]);
const snake = ref([{ x: 10, y: 10 }]);
const food = ref({ x: 5, y: 5 });
const direction = ref('right');
const gameInterval = ref(null);
const gameOver = ref(false);

const createGameBoard = () => {
    for (let i = 0; i < 20; i++) {
        const row = [];
        for (let j = 0; j < 20; j++) {
            row.push(0);
        }
        gameBoard.value.push(row);
    }
};

const getCellClass = (rowIndex, colIndex) => {
    const cellClass = {
        'cell': true
    };
    if (isSnake(rowIndex, colIndex)) {
        cellClass['snake'] = true;
    } else if (isFood(rowIndex, colIndex)) {
        cellClass['food'] = true;
    }
    return cellClass;
};

const isSnake = (rowIndex, colIndex) => {
    return snake.value.some(cell => cell.x === rowIndex && cell.y === colIndex);
};

const isFood = (rowIndex, colIndex) => {
    return food.value.x === rowIndex && food.value.y === colIndex;
};

const startGame = () => {
    gameInterval.value = setInterval(moveSnake, 200);
};

const moveSnake = () => {
    if (gameOver.value) return;
    const head = { ...snake.value[0] };
    switch (direction.value) {
        case 'up':
            head.x -= 1;
            break;
        case 'down':
            head.x += 1;
            break;
        case 'left':
            head.y -= 1;
            break;
        case 'right':
            head.y += 1;
            break;
    }
    snake.value.unshift(head);
    if (!isFood(head.x, head.y)) {
        snake.value.pop();
    } else {
        generateFood();
    }
    if (isCollision() || isOutOfBounds(head.x, head.y)) {
        clearInterval(gameInterval.value);
        gameOver.value = true;
        alert('Game Over!');
    }
};

const generateFood = () => {
    food.value.x = Math.floor(Math.random() * 20);
    food.value.y = Math.floor(Math.random() * 20);
};

const isCollision = () => {
    const head = snake.value[0];
    return snake.value.slice(1).some(cell => cell.x === head.x && cell.y === head.y);
};

const isOutOfBounds = (x, y) => {
    return x < 0 || x >= 20 || y < 0 || y >= 20;
};

onMounted(() => {
    createGameBoard();
});

onUnmounted(() => {
    clearInterval(gameInterval.value);
});
</script>

<style scoped>
#game-board {
    width: 400px;
    height: 400px;
    border: 1px solid black;
    display: grid;
    grid-template-columns: repeat(20, 1fr);
}

.cell {
    width: 20px;
    height: 20px;
    border: 1px solid #ccc;
    background-color: white;
}

.snake {
    background-color: green;
}

.food {
    background-color: red;
}
</style>