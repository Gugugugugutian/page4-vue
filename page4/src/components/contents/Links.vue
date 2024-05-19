<script>
export default {
    name: 'Links',  
    props: {
        links: {
            type: Array,
            default: //[
                [
                    // 请不要修改这里的链接，否则会影响该元素的复用
                    {n: 'undefined', u: undefined},
                    {n: 'undefined', u: undefined},
                ], 
            //]
        },
    },
}
</script>

<template>
    <div class="links">
        <a class="link" v-for="(link, index) in links" :key="index" :href="link.u">{{link.n}}</a>
    </div>
</template>

<style>
.links {
    max-height: 100%;
    text-align: center;
    line-height: 48px;
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    justify-content: start;
    margin: 0 0 15px 0;
}
.link {
    min-width: 125px;
    padding: 0 5px;
    display: block;
    overflow: hidden;
    font-size: 20px;
    border-radius: 5px;
    word-break: keep-all;
    text-decoration: none;
    color: inherit;
}
.link:hover {
    background-color: rgba(0, 0, 0, 0.1);
}
</style>