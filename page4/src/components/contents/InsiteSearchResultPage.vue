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
            const sites = this.insitePages.flat(Infinity);
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
        }
    }
}
</script>
<template>
    <div class="insite-result-page" v-show="searchShow">
        <p>{{ searchText }} 的站内搜索结果：共{{ this.result.length }}条 <button @click="hideResultPage">Close</button></p>
        <div v-for="(item, index) in result" style="padding-bottom: 2px;">
            <a :href="item.u">点击进入</a> ({{ index+1 }}) &#9;&#9; {{ item.n }}<br/>
        </div>
        <p>您可点击上方Close按钮关闭搜索结果</p>
    </div>
</template>
<style>
.insite-result-page a:hover {
    color: darkblue;
    background-color: whitesmoke;
}
.insite-result-page a {
    display: inline-block;
    padding: 3px;
    color: whitesmoke;
    background-color: darkblue;
    border-radius: 5px;
    text-decoration: none;
}
.insite-result-page {
    z-index: 999999;
    position: fixed;
    top: 0;
    left: 10vi;
    width: 80vi;
    min-height: 100vh;
    overflow-y: scroll;
    color: whitesmoke;
    background-color: rgba(0,0,0,0.7);
    padding: 15px;
}
</style>