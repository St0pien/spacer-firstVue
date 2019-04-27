<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo">
                <img src="https://3c1703fe8d.site.internapcdn.net/newman/csz/news/800/2018/nasacallsfor.jpg">
            </div>
            <div class="description">
                <h2 class="title">Lorem ipsum</h2>
                <p class="description">
                    laksjd l;askjdf;oa ij;oaslikdjla;sk dlfkjasldk fjas;ldkfja
                    asdjf ;asfj alskjf;aksdfakd flaski fl;asjdflasikdfja
                    lasdj fl;asdjf laksdjfl aisdf;laksjdl;fasjl; askjdfidjfalsasjdhfkasjdh
                    shdkf haskdjhf kasjdfhkasdh faksjdhfkasf kajskasdh askjhs
                </p>
            </div>
        </div>
        <div class="close" @click="$emit('closeModal')" />
    </div>
</template>

<script>
export default {
    name: 'Modal'
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
    }

    .close {
        position: absolute;
        width: 30px;
        height: 30px;
        right: 0;
        top: 0;
        cursor: pointer;

        &::before,
        &::after {
            position: absolute;
            top: 30px;
            right: 20px;
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
        display: flex;
        height: 100%;
        padding: 50px;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }

    .photo {
        width: 100%;
        height: auto;
        background: black;
    }

    img {
        width: 100%;
    }

    .description {
        color: #333;
    }
</style>
