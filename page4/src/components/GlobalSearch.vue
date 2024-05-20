<script> 
import InsiteSearchResultPage from '@/components/contents/InsiteSearchResultPage.vue'
export default {
    components: {
        InsiteSearchResultPage,
    },
    props: {
        windowWidth: {
            type: Number,
            default: 0,
        },
        insitePages: {
            type: Array,
            default: [],
        }, 
        dark: {
            type: Boolean,
            default: true,
        }
    },
    data() {
        return {
            showSearchWidget: false,
            showInsiteSearchResultPage: false,
            searchText: '',
            engine: 'Google',
        }
    },
    methods: {
        switchEngine() {
            if(this.engine == 'Google') {
                this.engine = 'Bing';
            } else if(this.engine == 'Bing') {
                this.engine = 'In-Site';
            } else {
                this.engine = 'Google';
            }
        },
        search() {
            if(this.searchText.length > 0) {
                if(this.engine == 'Google') {
                    window.open('https://www.google.com/search?q=' + this.searchText);
                } else if (this.engine == 'Bing') {
                    window.open('https://cn.bing.com/search?q=' + this.searchText);
                } else {
                    this.showInsiteSearchResultPage = true;
                }
            }
        }, 
        reverseShow() {
            if(this.showSearchWidget) this.hideInsiteResult();
            this.showSearchWidget = !this.showSearchWidget;
        }, 
        hideInsiteResult() {
            this.showInsiteSearchResultPage = false;
        }
    },
    computed: {
        searchContainerShow() {
            if(!this.showSearchWidget) {
                return 'top: -100vh;';
            } else {
                return 'top: 0;';
            }
        },
        searchIconRowPosition() {
            // if(!this.showSearchWidget) {
                if(this.windowWidth > 900) {
                    return 'left:30px';
                } else {
                    return 'right:30px';
                }
            // } else {
                // return 'left:' + Math.floor(this.windowWidth/2 - 40) + 'px';
            // }        
        },
    }, 
}
</script>
<template>
    <div class="search-icon" :class="{ dark: dark }" @click="reverseShow" :style="searchIconRowPosition">
        <div v-show="showSearchWidget">关闭</div>
        <div v-show="!showSearchWidget">搜索</div>
    </div>
    <div class="search-container" :class="{ dark1: dark }" :style="searchContainerShow">
        <input class="search-input" type="text" v-model="searchText" @keyup.enter="search">
        <div class="button-container">
            <button class="search-button" @click="switchEngine">Switch</button>
            <button class="search-button" @click="search">{{ engine }}</button>
        </div>
    </div>
    <InsiteSearchResultPage :insitePages="insitePages" :searchShow="showInsiteSearchResultPage" :searchText="searchText" @close-result-page='hideInsiteResult'></InsiteSearchResultPage>
</template>
<style>
.button-container button:hover {
    color: wheat;
    background-color: rgba(50, 50, 50, 0.55);
}
.button-container button {
    display: block;
    min-width: 100px;
    height: 50px;
    border: 0;
    color: whitesmoke;
    background-color: transparent;
    border-radius: 10px;
    font-size: 24px;
    padding: 15px 0px;
}
.button-container {
    padding: 15px 0;
    width: 60vi;
    max-width: 800px;
    display: flex;
    justify-content: end;
    align-items: center;
}
.search-container input {
    width: 60vi;
    max-width: 800px;
    font-size: 24px;
    height: 50px;
    color: whitesmoke;
    border: solid 2px whitesmoke;
    background-color: rgba(0, 0, 0, 0.35);
    border-radius: 10px;
    transition: background 1s ease-in-out,
                color 1s ease-in-out;
    padding: 0 15px;
}
.search-container input:focus {
    color: black;
    background-color: whitesmoke;
    outline: 0;
}
.search-container {
    z-index: 99998;
    transition: all 1s ease-in-out;
    position: fixed;
    top: 0;
    left: 0;
    width: 100vi;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.search-icon {
    position: fixed;
    top: 130px;
    z-index: 99999;
    background-color: yellowgreen;
    color: black;
    opacity: 0.85;
    height: 80px;
    width: 80px;
    border-radius: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
}
.dark .search-icon {
    background-color: green;
    color: whitesmoke;
    border: 0;
}
.search-icon:hover {
    opacity: 1;
}
</style>