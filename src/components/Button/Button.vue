<template>
    <div :class="btnClass" :style="`width: ${width}px`">
        <img :alt="type" :src="icon" />
    </div>
</template>

<script>
import SvgIcons from "@/components/Button/SvgIcons";
export default {
    name: "Button",
    props:{
        type: {
            type: String,
            default: 'add' // add, delete, edit
        },
        width: {
            type: Number, // 按钮宽度
            default: 30
        }
    },
    mounted() {},
    computed: {
        icon(){
            return SvgIcons[this.type]
        },
        btnClass(){
            let btnMap = new Map([
                ['edit', 'green'],
                ['delete', 'red'],
                ['close', 'red'],
                ['copy', 'blue'],
                ['share', 'blue'],
            ])
            return ['btn', btnMap.get(this.type)]
        }
    }
}
</script>

<style lang="scss">
@import "../../assets/scss/plugin";

$width-btn: 26px;
.btn{
    user-select: none;
    flex-grow: 0;
    flex-shrink: 0;
    width: $width-btn;
    height: $width-btn;
    @include border-radius($width-btn);
    overflow: hidden;
    padding: 2px;
    background-color: transparentize(black, 0.9);
    @extend .btn-like;
    img{
        display: block;
        width: 100%;
        height: 100%;
    }
    &.red{
        @include transition(background 0.3s);
        &:hover{
            @include transition(background 0.1s);
            background: transparentize($red, 0.2);
        }
    }
    &.green{
        @include transition(background 0.3s);
        &:hover{
            @include transition(background 0.1s);
            background: transparentize($green, 0.2);
        }
    }
    &.blue{
        @include transition(background 0.3s);
        &:hover{
            @include transition(background 0.1s);
            background: transparentize($blue, 0.2);
        }
    }
    &.orange{
        @include transition(background 0.3s);
        &:hover{
            @include transition(background 0.1s);
            background: transparentize($orange, 0.2);
        }
    }
}
</style>
