<script>
import Links from '@/components/contents/Links.vue'
export default {
    name: 'rightCircle', 
    data() {
        return {
            index: 0,
            linkPages: [
                [
                    {u: "https://chat.openai.com/chat", n: "ChatGPT",}, 
                    {u: "https://github.com/", n: "Github",},
                    {u: "https://singlelogin.se/", n: "ZLibrary",},
                    {n: 'GMail', u: 'https://mail.google.com/'},
                    {n: 'QQMail', u: 'https://mail.qq.com/'},
                    {n: '菜鸟教程', u: 'https://www.runoob.com/'},
                    {n: "WHU图书馆", u: "https://www.lib.whu.edu.cn/",}, 
                    {n: 'WHU信息门户', u: 'https://ehall.whu.edu.cn/new/index.html#/'},
                    {n: 'Leetcode', u: 'https://leetcode.cn/problemset/all/'},
                    {n: 'iiiLab', u: 'https://bili.iiilab.com/'},
                    {n: "高德地图",u: 'https://ditu.amap.com/', },
                    {n: "Bilibili",u: 'https://www.bilibili.com/', },
                    {n: "雀魂麻将",u: 'https://game.maj-soul.net/1/', },
                    {n: "Steam历史价格",u: 'https://steamdb.info/', },
                    {n: "科学上网",u: 'https://ikuuu.org/', },
                ],[
                    {n: "value2",u: 'undefined', },
                ],
            ], 
            linkTitles: [
                '常用', 
                '校园', 
                '文档',
            ]
        }
    },
    components: {
        Links,
    },
    props: {
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
            // 保证内容显示区域大小不变
            return 'padding-left: ' + (Math.max(0, 800-this.windowWidth)+15) + 'px; height: ' + Math.max(550, (800*550/this.windowWidth)) + 'px;';
        },
        circleh() {
            // 保证圆的高度可以容纳内容区域
            return 'height: ' + Math.max(1000, 350+(800*650/this.windowWidth)) + 'px;';
        }, 
        linkh1() {
            if(this.linkPages.length > this.index) return this.linkTitles[this.index]; 
            else return 'Overflow';
        }
    }
}
</script>
<template>
    <div class="circler" :style="circleh">
        <div class="circle-r-content" :style="maxw">
            <h1 class="rc-head">
                <span @click="indexMinus"><-</span> {{linkh1}} <span @click="indexAdd">-></span>
            </h1>
            <hr style="margin-bottom: 5px; width: 550px;"/>
            <Links :links="linkPages" :index="index"></Links>
            <p>这里可以再加一个条件过滤器</p>
        </div>
    </div>
</template>
<style>
.circle-r-content {
    margin-top: 290px;
    margin-left: 100px;
    max-width: 600px;
    display: flex;
    flex-direction: column;
    justify-content: start;
    align-items: center;
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
    /* margin: 0 auto; */
    margin-left: 15px;
    padding-bottom: 7px;
}
.rc-head span:hover {
    background-color: rgba(0, 0, 0, 0.1);
    color: green;
}
.dark .rc-head span:hover {
    color: aquamarine;
}
</style>