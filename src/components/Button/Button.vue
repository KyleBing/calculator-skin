<template>
    <div class="btn" :style="`width: ${width}px`">
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
    data(){
        return{
            icon: null
        }
    },
    mounted() {

    },
    computed: {
        icon(){
            return SvgIcons[this.type]
        }
    }
}
</script>

<style scoped lang="scss">
@import "../../assets/scss/plugin";
.btn{
    //border: 1px solid #888;
    @include border-radius(30px);
    overflow: hidden;
    padding: 0;
    background: linear-gradient(to bottom, #888, #666);
    //background-color: #888;
    @extend .btn-like;
    img{
        display: block;
        width: 100%;
    }
    &:hover{
        background: linear-gradient(to top, $magenta, lighten($magenta, 10%));
    }
}
</style>
