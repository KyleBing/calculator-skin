<template>
    <div class="copyright">
        <dl class="copyright-item">
            <dt>作者：</dt>
            <dd><a href="https://kylebing.cn">kylebing.cn</a></dd>
        </dl>
        <dl class="copyright-item">
            <dt>版本：</dt>
            <dd>{{version}}</dd>
        </dl>
    </div>
</template>

<script>
import projectConfig from '@/../package.json'
export default {
    name: "Copyright",
    data(){
        return {
            version: projectConfig.version
        }
    },
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
