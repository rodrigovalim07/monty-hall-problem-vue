<template>
    <div id="app">
        <h1>Problema de Monty Hall</h1>
        <div class="form">
            <div v-if="!started">
                <label for="portsAmount">Quantas portas? </label>
                <input type="text" id="portsAmount" size="3"
                    v-model.number="portsAmount">
            </div>
            <div v-if="!started">
                <label for="selectedPort">Qual porta é premiada? </label>
                <input type="text" id="selectedPort" size="3"
                    v-model.number="selectedPort">
            </div>
            <button v-if="!started" @click="started = true">Iniciar</button>
            <button v-if="started" @click="started = false; hasWon = false">Reiniciar</button>
        </div>
        <div class="doors" v-if="started">
            <div v-for="i in portsAmount" :key="i">
                <Door :hasGift="i === selectedPort" :number="i" @open="checkDoor(i)" />
            </div>
        </div>
        <div v-if="hasWon" class="winner-message">
            <h2>Você ganhou o prêmio!</h2>
        </div>
    </div>
</template>

<script>
import Door from './components/Door'

export default {
    name: 'App',
    components: { Door },
    data: function() {
        return {
            started: false,
            portsAmount: 3,
            selectedPort: null,
            hasWon: false
        }
    },
    methods: {
        checkDoor(number) {
            if (number === this.selectedPort) {
                this.hasWon = true;
            }
        }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

* {
    box-sizing: border-box;
    font-family: 'Montserrat', sans-serif;
}

body {
    color: #FFF;
    background: linear-gradient(to right, #836FFF, #00BFFF, #836FFF);
}

#app {
    display: flex;
    flex-direction: column;
    align-items: center;
}

#app h1 {
    border: 1px solid #000;
    background-color: #0004;
    padding: 20px;
    margin-bottom: 60px;
}

.form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 40px;
}

.form, .form input, .form button {
    margin-bottom: 10px;
    font-size: 2rem;
}

.doors {
    align-self: stretch;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
}

.winner-message {
    font-size: 40px;
    margin-top: 20px;
    text-align: center;
    color: #FFD700;
    font-weight: bold;
    background-clip: text;
    -webkit-background-clip: text;
    animation: glowing 1s infinite ease-in-out;
}

@keyframes glowing {
    0% { text-shadow: 0 0 10px #ff6b6b, 0 0 20px #ff6b6b, 0 0 30px #ff6b6b, 0 0 40px #ff6b6b, 0 0 50px #ff6b6b; }
    50% { text-shadow: 0 0 20px #f06595, 0 0 30px #f06595, 0 0 40px #f06595, 0 0 50px #f06595, 0 0 60px #f06595; }
    100% { text-shadow: 0 0 10px #ab83f7, 0 0 40px #ab83f7, 0 0 50px #ab83f7, 0 0 60px #ab83f7, 0 0 70px #ab83f7; }
}
</style>