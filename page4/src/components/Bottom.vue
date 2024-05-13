<script>
export default {
    name: 'Bottom',
    data() {
        return {
        }
    },
    props: {
        ipInfo: {
            type: Object,
            default: () => ({})
        }
    },
}
</script>
<template>
    <div class="bottom">
        <div>
            {{ ipInfo.city }}, {{ ipInfo.country_name }}. ({{ipInfo.ipv4}})
        </div>
    </div>
</template>
<style>
.bottom {
    z-index: 9999;
    position: fixed;
    bottom: 0;
    width: 100vi;
    height: 30px;
    padding: 0 20px;

    background-color: rgba(0, 0, 0, 0.5);

    display: flex;
    justify-content: center;
}
</style>