<template>
    <div class="instructions">
        <h3>使用说明</h3>
        <p>本计算器应用对算式的兼容比较强，因为平时用键盘打正常的算式会非常麻烦。</p>
        <p>所以我添加了转义的快捷输入：</p>
        <table>
            <thead>
                <tr><th>输入</th><th>会转成</th></tr>
            </thead>
            <tbody>
                <tr><td>j</td><td>加号 +</td></tr>
                <tr><td>x</td><td>乘号 *</td></tr>
                <tr><td>c</td><td>除号 ÷</td></tr>
                <tr><td>[]</td><td>括号 ()</td></tr>
            </tbody>
        </table>
        <p>比如 3x4j45x[5j6]c6 就会变成 3×4+45×(5+6)÷6</p>
    </div>
</template>

<script>
import projectConfig from '@/../package.json'
export default {
    // 使用说明
    name: "Instructions",
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
.instructions{
    margin-bottom: 10px;
    font-size: 10px;
}
h3 {

}
table{
    margin-top: 5px;
    margin-bottom: 5px;
    border-collapse: collapse;
    th, td{
        min-width: 50px;
        padding: 2px 3px;
        border-collapse: collapse;
        border: 1px solid $color-border;
        text-align: center;
    }
}
p{
    margin-bottom: 2px;
    margin-top: 0;
    line-height: 1.2;
}

</style>
