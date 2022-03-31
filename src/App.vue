<template>
    <div class="container">
        <Display class="mb-2" :equation="equation" :result="result"/>
        <div class="equation mb-2">
            <input @keydown.enter="calculate" placeholder="请输入算式" v-model="equation"/>
            <Button type="add" :width="55" @click="addResult"/>
        </div>
        <ResultList :resultList="resultList" @delete="deleteResultAt"/>
    </div>
</template>

<script>

import Display from "@/components/Display";
import calculator from "advanced-calculator"
import ResultList from "@/components/ResultList";
import Button from "@/components/Button/Button";

export default {
    name: 'App',
    components: {Button, ResultList, Display },
    data(){
        return {
            equation: '', // 算式
            result: '', // 计算结果,
            resultList: [], // 计算结果保存列表
        }
    },
    methods: {
        calculate(){
            this.equation = this.equation.replaceAll(/[xX]/g,'*')
            if (this.equation){ // 算式不为空
                let result = calculator.evaluate(this.equation)
                if (typeof(result) === 'string' ){
                    this.result = '输入有误'
                } else {
                    this.result = String(result)
                    // this.result = result.toFixed(2)
                }
            } else {

            }

        },
        addResult(){
            if (this.equation && this.result){
                this.resultList.unshift({
                    date: new Date(),
                    equation: this.equation,
                    result: this.result,
                })
            }
        },
        deleteResultAt(index){
            this.resultList.splice(index ,1)
        }
    },
}
</script>

<style lang="scss" scoped>
@import "src/assets/scss/gutter";
@import "src/assets/scss/plugin";

.container{
    padding: 30px;
}

.equation{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-flow: row nowrap;
    input{
        width: 100%;
        display: block;
        text-align: center;
        font-size: 30px;
        padding: 10px 20px;
        border: 3px solid $color-border;
        @include border-radius(5px);
        outline: none;
        &:focus{
            border-color: $color-border-highlight;
        }
    }
}
.btn{
    @include border-radius(5px);
    padding: 3px 5px;
    border: 1px solid $color-border;
    @extend .btn-like
}
</style>
