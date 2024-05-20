<script>
export default {
    name: 'InsiteSearchResultPage',
    props: {
        searchText: {
            type: String,
            default: '',
        },
        searchShow: {
            type: Boolean,
            default: false,
        },
        insitePages: {
            type: Array,
            default: [],
        }
    },
    emits: ['close-result-page'],
    data() {
        return {
            result: [],
        }
    },
    methods: {
        doSearch(text) {
            // 搜索字段
            const seq = text.trim().toLowerCase().split(' ');
            // 生成搜索字段的正则表达式，用于后续对每个链接做匹配
            const regex = new RegExp(seq.join('|'), 'i');
            // 网站链接
            const sites = new Set(this.insitePages.flat(Infinity));
            // 搜索
            this.result = [...new Set([...sites].filter(site => (regex.test(site.n)))
                .concat([...sites].filter(site => (((site.en!==undefined)&&regex.test(site.en))))))];
        },
        hideResultPage() {
            this.$emit('close-result-page');
        }
    },
    watch: {
        searchShow(newVal) {
            if(newVal) {
                this.doSearch(this.searchText);
            }
        },
    },
    computed: {
        googleSearchLink() {
            return 'https://www.google.com/search?q=' + this.searchText;
        },
        bingSearchLink() {
            return 'https://cn.bing.com/search?q=' + this.searchText;
        }
    }
}
</script>
<template>
    <div class="insite-result-page" v-show="searchShow">
        <button id="btnisp1" @click="hideResultPage">&times;</button>
        <p>{{ searchText }} 的站内搜索结果：共{{ this.result.length }}条</p>
        <div class="insite-results">
            <span class="insite-result" v-for="(item, index) in result" style="padding-bottom: 6px;">
                <span style="width: 30px; display: inline-block;">{{ index+1 }}.</span><a style="width: 160px; text-align: center;" :href="item.u">{{ item.n }}</a>
            </span>
        </div>
        <p>如需关闭，请点击右上方红色关闭按钮。</p>
        <p>没有找到？试试：
            <a :href="googleSearchLink">去Google搜索</a>&nbsp;
            <a :href="bingSearchLink">去Bing搜索</a>
        </p>
    </div>
</template>
<style>
#btnisp1:hover {
    background-color: orangered;
}
#btnisp1 {
    background-color: red;
    width: 48px;
    height: 48px;
    font-size: 36px;
    color: whitesmoke;
    border: 3px solid whitesmoke;
    border-radius: 24px;
    position: absolute;
    top: 20px;
    right: 20px;
}
.insite-results {
    font-size: 16px; 
    line-height: 20px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}
.insite-result {
    width: 200px;
}
.insite-result-page a:hover {
    color: darkgreen;
    background-color: whitesmoke;
}
.insite-result-page a {
    display: inline-block;
    padding: 3px;
    color: whitesmoke;
    background-color: rgb(3, 74, 3);
    border-radius: 5px;
    text-decoration: none;
}
.insite-result-page {
    z-index: 999999;
    position: fixed;
    top: 0;
    left: 10vi;
    width: 80vi;
    height: 100vh;
    overflow-y: scroll;
    color: whitesmoke;
    background-color: rgba(0,0,0,0.7);
    padding: 15px;
}
</style>