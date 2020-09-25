<template>
    <div id="app">
        <div class="container">
            <div class="timer-list">
                <timer v-for="item in array"
                       :key="item"></timer>
                <button class="add-timer" @click="addTimer">+</button>
            </div>
        </div>
    </div>
</template>

<script>
    import timer from "./components/timer";

    export default {
        name: 'App',
        components: {
            timer,
        },
        data() {
            return {
                array: [],
                increment: 0,
            }
        },
        methods: {
            addTimer: function () {
                const value = ++this.increment;
                this.array.push(value);
            }
        },
    }
</script>

<style>
    *,
    *:after,
    *:before {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    body {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        text-align: center;
        color: #9E9E9E;
        background-color: #353638;
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    .container {
        padding-top: 72px;
    }

    .timer-list {
        max-width: 1024px;
        margin: 0 auto;
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-gap: 50px;
        justify-items: center;
    }

    @media screen and (max-width: 768px) {
        .timer-list {
            grid-template-columns: repeat(2, 1fr);
        }
    }

    @media screen and (max-width: 320px) {
        .timer-list {
            grid-template-columns: repeat(1, 1fr);
        }
    }

    .add-timer {
        width: 225px;
        height: 120px;
        border: none;
        outline: none;
        background-color: #696969;
        color: #9E9E9E;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        font-size: 30px;
        line-height: 21px;
        cursor: pointer;
    }
</style>
