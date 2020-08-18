<template>
    <div class="carrousel">
        <slot></slot>
        <button class="carrousel__nav carrousel__next" @click.prevent="next"></button>
        <button class="carrousel__nav carrousel__prev" @click.prevent="prev"></button>
        <div class="carrousel__pagination">
            <button v-for="n in slidesCount" @click="goto(n-1)" :class="{active: n-1 == index}"></button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                index: 0,
                slides: [],
                direction: null
            }
        },
        computed: {
            slidesCount () { return this.slides.length }
        },
        watch: {
            slides (slides) {
                if( this.index >= this.slidesCount) {
                    this.index = this.slidesCount - 1;
                }
            }
        },
        methods: {
            next() {
                this.index++
                this.direction = 'right'
                if(this.index >= this.slidesCount) {
                    this.index = 0
                }
            },
            prev() {
                this.direction = 'left'
                this.index--
                if(this.index < 0) {
                    this.index = this.slidesCount - 1;
                }
            },
            goto (index) {
                this.direction = index > this.index ? 'right' : 'left'
                this.index = index
            }
        },
        mounted() {
            this.slides = this.$children
        },

    }
</script>

<style>
    .carrousel {
        position: relative;
        overflow: hidden;
    }

    .carrousel__nav {
        position: absolute;
        top: 50%;
        margin-top: 31px;;
        left: 10px;
        background: url(prev.png);
        width: 63px;
        height: 63px;


    }

    .carrousel__nav.carrousel__next {
        right: 10px;
        left: auto;
        background: url(next.png);
    }

    .carrousel__pagination {
        position: absolute;
        bottom: 10px;
        left: 0;
        right: 0;
        text-align: center;
    }

    .carrousel__pagination button {
        display: inline-block;
        width: 10px;
        height: 10px;
        background-color: #000;
        opacity: 0.8;
        border-radius: 10px;
        margin: 0 2px
    }

    .carrousel__pagination button.active{
        background-color: #FFF;
    }

</style>