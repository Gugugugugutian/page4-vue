<script>
export default {
    name: 'DayNight',
    data() {
        return {
            dark: false
        }
    },
    emits: ['switch-dark'],
    mounted() {
        this.dark = window.matchMedia('(prefers-color-scheme: dark)').matches;
    },
    methods: {
        switchDark() {
            this.dark = !this.dark;
            this.$emit('switch-dark', this.dark);
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
    background-color: orange;
    border: 2px solid black;
    left: -2px;
}
.night-s {
    background-color: darkblue;
    border: 2px solid white;
    left: 18px;
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