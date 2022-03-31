<template>
    <div class="container">
        <Display class="mb-2" :equation="equation" :result="result"/>
        <div class="equation mb-2">
            <input @keydown.enter="addResult" placeholder="请输入算式" v-model="equation"/>
<!--            <Button type="add" :width="55" @click="addResult"/>-->
<!--            <Button type="menu" :width="55" @click="calculate"/>-->
        </div>
        <ResultList :resultList="resultList" @edit="editResultAt" @delete="deleteResultAt"/>
        <Copyright/>
    </div>
</template>

<script>

import Display from "@/components/Display";
import calculator from "advanced-calculator"
import ResultList from "@/components/ResultList";
import Button from "@/components/Button/Button";
import ClipboardJS from "clipboard";
import Copyright from "@/components/Copyright";

export default {
    name: 'App',
    components: {Copyright, Button, ResultList, Display },
    data(){
        return {
            equation: '', // 算式
            result: '', // 计算结果,
            resultList: [], // 计算结果保存列表
        }
    },
    methods: {
        // 计算结果
        calculate(){
            this.equation = this.equation.replaceAll(/[xX]/g,'*')

            console.log('---about to excute calculation: ', this.equation)
            let result = calculator.evaluate(this.equation)
            if (this.equation !== ''){
                if (typeof(result) === 'string' ){
                    this.result = '输入有误'
                } else {
                    this.result = String(result)
                    // this.result = result.toFixed(2)
                }
            }

        },
        // 添加结果到结果集
        addResult(){
            if (this.equation && this.result && this.equationIsValid(this.equation)){
                this.resultList.unshift({
                    date: new Date(),
                    equation: this.equation.replaceAll(' ','').replaceAll(/([\+\-\(\)])/g, ' $1 '),
                    // equation: this.equation.replaceAll(' ','').replaceAll(/([\+\-\/\*\(\)])/g, ' $1 '),
                    result: this.result,
                })
            }
        },
        // 删除 index 位置的记录
        deleteResultAt(index){
            this.resultList.splice(index ,1)
        },

        // 重新编辑 index 位置的算式
        editResultAt(index){
            let editResult = this.resultList[index]
            this.equation = editResult.equation
        },

        // 验证算式是否可用
        equationIsValid(equation){
            return /^[\.\d].*\d+ *\)?$/i.test(equation)
        }
    },
    watch: {
        equation(newValue){
            if (this.equationIsValid(newValue)){
                console.log('valid equation', newValue)
                this.calculate()
            }
        }
    },

    mounted() {
        // 绑定剪贴板操作方法
        this.clipboard = new ClipboardJS('.clipboard', {
            text: function (trigger) {
                return trigger.getAttribute('dataClipboard')
            },
        })
        this.clipboard.on('success', ()=>{  // 还可以添加监听事件，如：复制成功后提示
            console.log('copy success')
        })
    },

    beforeUnmount() {
        this.clipboard.destroy() // 销毁 clipboard 避免弹出多个复制成功提示框
    },

}
</script>

<style lang="scss" scoped>
@import "src/assets/scss/gutter";
@import "src/assets/scss/plugin";

.container{
    font-family: Verdana;
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
