<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo">
                <img :src="photo" :alt="title">
            </div>
            <div class="description">
                <h2 class="title">{{ title }}</h2>
                <p class="description">
                    {{ description }}
                </p>
            </div>
        </div>
        <div class="close" @click="$emit('closeModal')" />
    </div>
</template>

<script>
/* eslint-disable */
export default {
    name: 'Modal',
    data() {
        return {
            photo: null,
            title: null,
            description: null
        };
    },
    props: {
        item: {
            type: Object,
            required: true
        }
    },
    mounted() {
        this.photo = this.item.links[0].href;
        this.title = this.item.data[0].title;
        this.description = this.item.data[0].description;
    }
}
</script>

<style lang="scss" scoped>
    .outerWrapper {
        background: #f6f6f6;
        max-width: 100%;
        height: 100%;
        position: fixed;
        top: 0;
        left: 0;

        @media (min-width: 1024px) {
            max-width: 70%;
            height: 60%;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            margin: auto;
            box-shadow: 0 30px 30px -10px rgba(0,0,0, .3);
        }
    }

    .close {
        position: absolute;
        width: 30px;
        height: 30px;
        right: 30px;
        top: 30px;
        cursor: pointer;

        &::before,
        &::after {
            position: absolute;
            top: 0;
            right: 0;
            content: '';
            width: 10px;
            height: 2px;
            background: black;
            display: block;
        }

        &::before {
            transform: rotate(45deg);
        }

        &::after {
            transform: rotate(-45deg);
        }
    }

    .innerWrapper {
        overflow: auto;
        display: flex;
        height: 100%;
        padding: 50px;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        background: linear-gradient(white, 70%, rgb(124, 119, 119));

        @media (min-width: 1024px) {
            flex-direction: row;

            .photo {
                min-width: 50%;
                margin-right: 20px;
            }
        }
    }

    .photo {
        margin-top: 20vh;
        width: 100%;
        min-height: 30vh;
        height: auto;
        background: black;
        max-height: 100%;
        overflow: hidden;
    }

    img {
        width: 100%;
    }

    .description {
        color: #333;
    }

    div.description {
        max-height: 100%;
        max-width: 350px;
    }

    .title {
        color: #1e3d4a;
    }
</style>