<script>
export default {
    name: 'DayNight',
    data() {
        return {
            dark1: this.dark,
        }
    },
    props: {
        dark: {
            type: Boolean,
            default: false,
        }
    },
    emits: ['switch-dark'],
    methods: {
        switchDark() {
            this.dark1 = !this.dark1;
            this.$emit('switch-dark', this.dark1);
        }
    }
}
</script>

<template>
    <div class="day-night">
        <div :class="{ 'day-b': !dark, 'night-b': dark }" class="day-night-button" @click="switchDark">
            <div class="day-night-switch" :class="{ 'day-s': !dark, 'night-s': dark }">
            </div> 
        </div>
    </div>
</template>

<style>
.day-s {
    background-color: darkorange;
    left: -2px;
    box-shadow: 1px 1px 1px #000, -1px -1px 1px #fff;
}
.night-s {
    background-color: dodgerblue;
    left: 18px;
    box-shadow: 1px 1px 1px #fff, -1px -1px 1px #000;
}
.day-night-switch {
    top: -3.5px;
    position: relative;
    height: 24px;
    width: 24px;
    border-radius: 12px;
    transition: all 1s ease-in-out;
}
.day-b {
    border: 2px solid black;
    background-color: skyblue;
    box-shadow:
            inset -1px -1px 2px rgba(255, 255, 255, .9),
            inset 1px 1px 2px rgba(0, 0, 0, .4);
}
.night-b {
    border: 2px solid white;
    background-color: #333;
}
.day-night-button {
    height: 20px;
    margin: 2px;
    margin-right: 10px;
    width: 40px;
    border-radius: 10px;
    transition: all 1s ease-in-out;
}
</style>