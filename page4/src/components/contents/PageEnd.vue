<script>
import EndLinks from '@/components/contents/EndLinks.vue'
export default {
    props: {
        dark: {
            type: Boolean,
            default: false,
        },
    },
    data() {
        return {
            linkTitles: [
                '联系作者',
                '其他主页',
                '友情链接',
            ],
            links: [
                [
                    {name: 'Via Gmail', url: '@mailto:gutian2002@gmail.com'},
                    {name: 'Via WHUmail', url: '@mailto:gugugugugutian@whu.edu.cn'},
                ], [
                    {name: 'GitHub', url: 'https://github.com/gugugugugutian'},
                ], [
                    {name: 'StarkiJ', url: 'https://starkij.github.io/'},
                ],
            ],
            dictum: '拼搏改变命运，励志照亮人生', 
        }
    },
    components: {
        EndLinks,
    }
}
</script>

<template>
    <div class="page-end">
        <div style="width: 80vi; border-bottom: 1px solid; text-align: center; margin-bottom: 10px;"></div>
        <div class="page-end2">
            <div class="page-end1">
                <EndLinks v-for="(link, index) in links" :key="index" :links="link" :linkTitle="linkTitles[index]"></EndLinks>
            </div>
            <div class="page-end3">
                <h1> Gugugugugutian.github.io </h1>
                <p> 感谢您访问本站 </p>
            </div>
        </div>
    </div>
</template>
<style>
.page-end2 {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
}
.page-end1 {
    display: flex;
    flex-direction: row;
}
.page-end3 {
    display: flex;
    flex-direction: column;
    align-items: end;
}
.page-end {
    padding: 2vi 2vh;
}
</style>