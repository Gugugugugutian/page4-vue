<script>
export default {
    name: 'Links',  
    props: {
        index: {
            default: 0,
            type: Number,
        },
        windowWidth: {
            default: 0,
            type: Number,
        },
        links: {
            type: Array,
            default: [
                [
                    // 请不要修改这里的链接，否则会影响该元素的复用
                    {n: 'undefined', u: undefined},
                    {n: 'undefined', u: undefined},
                ], 
            ]
        },
    },
    computed: {
        curLinks() {
            if(this.links.length > this.index) return this.links[this.index]; 
            else return [[{n: 'OVERFLOW', u: undefined}]];
        },
    },
}
</script>

<template>
    <div class="links">
        <a class="link" v-for="(link, index) in curLinks" :key="index" :href="link.u">{{link.n}}</a>
    </div>
</template>

<style>
.links {
    text-align: center;
    line-height: 48px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin: 0 0 15px 0;
}
.link {
    min-width: 125px;
    padding: 0 5px;
    display: block;
    overflow: hidden;
    font-size: 20px;
    /* border: 1px solid; */
    border-radius: 5px;
    word-break: keep-all;
    text-decoration: none;
    color: inherit;
}
.link:hover {
    background-color: rgba(0, 0, 0, 0.1);
}
</style>