<template>
    <div class="equation mb-2">
        <input @keydown.enter="calculate" placeholder="请输入算式" v-model="equation"/>
    </div>
    <Display :equation="equation" :result="result"/>
    <div>{{tip}}</div>
</template>

<script>

import Display from "@/components/Display";
import calculator from "advanced-calculator"

export default {
    name: 'App',
    components: { Display },
    data(){
        return {
            equation: '', // 算式
            tip: '', // 提示
            result: '', // 计算结果
        }
    },
    methods: {
        calculate(){
            let result = calculator.evaluate(this.equation)
            if (typeof(result) === 'string' ){
                this.result = '输入有误'
            } else {
                this.result = result
                // this.result = result.toFixed(2)
            }
        }
    },
}
</script>

<style lang="scss" scoped>
@import "src/assets/scss/gutter";
@import "src/assets/scss/plugin";
.equation{
    display: flex;
    align-items: center;
    flex-flow: column nowrap;
    input{
        text-align: center;
        font-size: 40px;
        padding: 10px 20px;
        border: 1px solid $color-border;
        @include border-radius(10px);
        &:focus{
            border-color: $color-border-highlight;
        }
    }
}
</style>
