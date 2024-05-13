<script>
export default {
    name: 'leftCircle', 
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
            return 'max-width: ' + this.windowWidth + 'px;';
        }
    }
}
</script>
<template>
    <div class="circlel">
        <div class="circle-l-content" :style="maxw">
            <h1>小工具</h1>
        </div>
    </div>
</template>
<style>
.circle-l-content {
    margin: 100px;
    height: 600px;
    display: flex;
    justify-content: center;
    align-items: center;
}
.circlel {
    width: 800px;
    height: 800px;
    border-radius: 50%;
    background-color: #d05e5e;
    opacity: 0.7;
}
.circlel:hover {
    opacity: 0.9;
}
</style>