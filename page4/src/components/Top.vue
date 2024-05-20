<script>
import DayNight from '@/components/icons/DayNight.vue'
export default {
    name: 'Top',
    components: {
        DayNight
    },
    data() {
        return {
            time: 'Time',
        }
    },
    props: {
        dark: {
            type: Boolean,
            default: undefined,
        },
        windowWidth: {
            type: Number,
            default: 0,
        },
        version: {
            type: String,
            default: 'Gitpage 测试版本'
        },
        title: {
            type: String,
            default: 'gugugugugutian'
        },
        showInfo: {
            type: Boolean,
            default: true
        },
    }, 
    emits: ['change-dark'],
    methods: {
        changeDark() {
            this.$emit('change-dark');
        }
    },
    mounted() {
        // 时间的显示
        this.time = new Date().toLocaleString();
        console.log("[Page4] Site loaded at: ", this.time);
        setInterval(() => {
            this.time = new Date().toLocaleString();
        }, 1000);
    },
}
</script>

<template>
    <div class="top">
        <DayNight :dark="dark" @switch-dark="changeDark" />

        <div class="top1">
            <div class="title" v-show="this.windowWidth>260">
                <h1>{{title}}</h1>
            </div>

            <div class="info" v-show="this.windowWidth>576">
                {{ time }}<br/> {{ version }}
            </div>
        </div>
    </div>
</template>

<style>
.info {
    text-align: right;
}
.top1 {
    width: 100%;
    display: flex;
    justify-content: space-between;
}
.top {
    position: fixed;
    width: 100%;
    padding: 2px 5vi;
    display: flex;
    flex-wrap: nowrap;
    align-items: center;
    height: 48px;
    max-height: 48px;
    overflow: hidden;
    word-break: keep-all;
}
.top h1 {
    padding: 0;
    line-height: 48px;
}
.info {
    line-height: 24px;
}
</style>