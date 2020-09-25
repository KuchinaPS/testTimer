<template>
    <div class="timer">
        <div class="timer_time">
            <div :class="changeNum" class="time_output">{{calcTime}}</div>
        </div>
        <div class="timer_control" :class="changeLine">
            <button class="btn btn-start" v-if="!isRunning" @click="timerOn"></button>
            <button class="btn btn-pause" v-else @click="timePause"></button>
            <button :class="changeStop" class="btn btn-stop" @click="timeStop"></button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "timer",
        data: function () {
            return {
                tics: 0,
                timerID: 0,
                isRunning: false,
            }
        },
        computed: {
            calcTime: function () {
                const second = this.tics % 60;
                const minutes = Math.floor(this.tics / 60);
                const formattedMin = minutes === 0 ? "" : `${minutes % 60}:`;
                const hours = Math.floor(this.tics / 3600);
                const formattedHour = hours === 0 ? "" : `${hours}:`;

                return `${formattedHour}${formattedMin}${second}`;
            },
            changeNum:function(){
               return this.isRunning ? "btn-active" : "";
            },
            changeStop:function(){
                return this.isRunning ? "btn-stop--active" : "";
            },
            changeLine:function(){
                return this.isRunning ? "timer-control--active" : "";
            }
        },
        methods: {
            timerOn: function () {
                this.timerID = setInterval(this.updateTime, 1000);
                this.isRunning = true;
            },
            updateTime: function () {
                this.tics += 1;
            },
            timePause: function () {
                this.isRunning = false;
                clearTimeout(this.timerID);
            },
            timeStop: function () {
                this.tics = 0;
                this.isRunning = false;
                clearTimeout(this.timerID);
            }
        }
    }

</script>

<style scoped>
    .timer {
        width: 225px;
        height: 120px;
        background-color: #696969;
        color: #9E9E9E;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        font-size: 22px;
        line-height: 21px;
    }
    .timer_control {
        display: flex;
        justify-content: center;
        align-items: center;
        position: relative;
    }
    .timer_control:before{
        content: "";
        position: absolute;
        width: 225px;
        height: 1px;
        left: 0;
        top: -20px;
        background-color:#9E9E9E;
    }
    .timer-control--active:before{
        content: "";
        position: absolute;
        width: 225px;
        height: 1px;
        left: 0;
        top: -20px;
        background-color:#ffffff;
    }

    .btn {
        background-color: transparent;
        border: none;
        outline: none;
        margin-right: 50px;
        position: relative;
        width: 20px;
        height: 20px;
        cursor: pointer;
    }

    .btn:last-child {
        margin-right: 0;
    }

    .btn:before,
    .btn:after {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
    }

    .btn-start:before {
        border: 10px solid transparent;
        border-left: 17px solid #9E9E9E;
    }

    .btn-stop:before {
        width: 20px;
        height: 20px;
        background-color: #9E9E9E;
    }
    .btn-stop--active:before {
        width: 20px;
        height: 20px;
        background-color: #ffffff;
    }

    .btn-pause:before {
        width: 3px;
        height: 20px;
        background-color: #ffffff;
    }

    .btn-pause:after {
        width: 3px;
        height: 20px;
        background-color: #ffffff;
        left: 6px;
    }
    .btn-active{
        color: #ffffff;
    }
</style>