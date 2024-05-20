<script>
import Links from '@/components/contents/Links.vue'
export default {
    name: 'rightCircle', 
    data() {
        return {
            index: 0,
        }
    },
    components: {
        Links,
    },
    props: {
        linkPages: {
            type: Array,
            default: [],
        }, 
        linkTitles: {
            type: Array,
            default: [],
        },
        windowWidth: {
            default: 0,
            type: Number,
        }
    },
    methods: {
        indexAdd() {
            this.index = this.index<(this.linkPages.length-1) ? this.index+1 : 0;
        }, 
        indexMinus() {
            this.index = this.index>0 ? this.index-1 : this.linkPages.length-1;
        },
    },
    computed: {
        maxw() {
            // 保证内容左右不越界
            return 'padding-left: ' + (Math.max(0, 800-this.windowWidth)+15) + 'px; height: ' 
            // 保证内容显示区域大小不变
                                    + Math.max(550, (800*550/this.windowWidth)) + 'px;';
        },
        circleh() {
            // 保证圆的高度可以容纳内容区域
            return 'height: ' + Math.max(1000, 350+(800*650/this.windowWidth)) + 'px;';
        }, 
        linkh1() {
            if(this.linkPages.length > this.index) return this.linkTitles[this.index]; 
            else return 'Overflow';
        },
        curLinks() {
            if(this.linkPages.length > this.index) return this.linkPages[this.index]; 
            else return [[{n: 'OVERFLOW', u: undefined}]];
        },
    },
}
</script>
<template>
    <div class="circler" :style="circleh">
        <div class="circle-r-content" :style="maxw">
            <h1 class="rc-head">
            <span @click="indexMinus"><-</span> {{linkh1}} <span @click="indexAdd">-></span>
            </h1>
            <Links :links="curLinks"></Links>
        </div>
    </div>
</template>
<style>
.circle-r-content {
    margin-top: 290px;
    margin-left: 100px;
    max-width: 600px;
    padding-bottom: 100px;
    display: flex;
    flex-direction: column;
    justify-content: start;
    align-items: start;
}
.circler {
    width: 1000px;
    border-radius: 500px;
    background-color: orange;
    opacity: 0.9;
    transition: background 1s ease-in-out;
}
.dark .circler {
    background-color: darkorange;
}
.rc-head {
    display: flex;
    justify-content: space-between;
    width: 300px;
    margin-left: 15px;
    padding-bottom: 7px;
    border-bottom: 2px solid;
}
.rc-head span:hover {
    background-color: rgba(0, 0, 0, 0.1);
    color: green;
}
.dark .rc-head span:hover {
    color: aquamarine;
}
</style>