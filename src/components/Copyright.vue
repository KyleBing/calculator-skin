<template>
    <div class="copyright">
        <dl class="copyright-item">
            <dt>作者：</dt>
            <dd><a href="https://kylebing.cn">kylebing.cn</a></dd>
        </dl>
        <dl class="copyright-item">
            <dt>版本：</dt>
            <dd>v1.00</dd>
        </dl>
    </div>
</template>

<script>
export default {
    name: "Copyright",
    props:{
        result: {
            type: String,
            default: ''
        },
        equation: {
            type: String,
            default: ''
        }
    }
}
</script>

<style scoped lang="scss">
@import "src/assets/scss/plugin";
.copyright{
    position: fixed;
    bottom: 10px;
    left: 20px;
}

dl.copyright-item{
    margin: 0;
    font-size: 10px;
    color: $text-subtitle;
    display: flex;
    justify-content: flex-start;
    dt{
        text-align: right;
    }
    dd{
        margin-inline-start: 0;
        text-align: left;
        a{
            color: inherit;
            text-decoration: none;
        }
        &:hover{
            a {
                text-decoration: underline;
                color: $magenta;
            }
        }
    }
}

</style>
