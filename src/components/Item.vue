<template>
    <div :style="style" class="item" />
</template>

<script>
export default {
    name: 'Item',
    props: {
        item: {
            type: Object,
            required: true,
        },
    },
    data() {
        return {
            photo: this.item.links[0].href,
        };
    },
    computed: {
        style() {
            return `background-image: url("${this.photo}")`;
        }
    }
};
</script>

<style lang="scss" scoped>
    .item {
        width: 40vw;
        height: 250px;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: 50%;
        box-shadow: 0 0 10px black;

        @media (min-width: 758px) {
            width: 25vw;
        }
    }
</style>