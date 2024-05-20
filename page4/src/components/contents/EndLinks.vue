<script>
export default {
    props: {
        links: {
            type: Array,
            default: [],
        },
        linkTitle: {
            type: String,
            default: '',
        },
        dark: {
            type: Boolean,
            default: false,
        },
    }
}
</script>
<template>
    <div class="end-links">
        <h2 class="end-links-title">{{linkTitle}}</h2>
        <a v-for="(link, index) in links" class="end-links-link" :key="index" :href="link.url" >
            {{link.name}}
        </a>
    </div>
</template>
<style>
.end-links {
    display: flex;
    flex-direction: column;
    width: 120px;
    padding-right: 5px;
}
.end-links-title {
    font-size: 16px;
}
.end-links a {
    opacity: 0.7;
    display: block;
    text-decoration: none;
    padding: 8px 0;
    color: black;
    border-radius: 8px;
    transition: color 1s ease-in-out;
}
.end-links a:hover {
    color: darkgreen;
    background-color: rgba(0,0,0,0.1);
}
.dark .end-links a {
    color: white;
}
.dark .end-links a:hover {
    color: greenyellow;
    background-color: rgba(255,255,255,0.1);
}
</style>