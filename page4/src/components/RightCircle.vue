<script>
export default {
    name: 'rightCircle', 
    data() {
        return {

        }
    },
    props: {
        windowWidth: {
            default: 0,
            type: Number,
        }
    },
    computed: {
        maxw() {
            // 保证内容左右不越界
            // 保证内容显示区域大小不变
            return 'padding-left: ' + Math.max(0, 800-this.windowWidth) + 'px; height: ' + Math.max(650, (800*650/this.windowWidth)) + 'px;';
        },
        circleh() {
            // 保证圆的高度可以容纳内容区域
            return 'height: ' + Math.max(1000, 350+(800*650/this.windowWidth)) + 'px;';
        }
    }
}
</script>
<template>
    <div class="circler" :style="circleh">
        <div class="circle-r-content" :style="maxw">
            <h1>内容区</h1>
        </div>
    </div>
</template>
<style>
.circle-r-content {
    margin: 250px 100px 100px 100px;
    height: 650px;
    display: flex;
    justify-content: center;
    align-items: center;
    /* background-color: beige; */
}
.circler {
    width: 1000px;
    /* height: 1000px; */
    border-radius: 500px;
    background-color: darkorange;
    opacity: 0.7;
}
.circler:hover {
    opacity: 0.9;
}
</style>