<template>
    <div class="container">
<!--        <Display class="mb-2" :equation="equation" :result="result"/>-->

        <div class="input-group-list">
            <h3>结果四舍五入</h3>
            <div class="input-group">
                <input v-model="accuracy" id="round0" :value="0" name="round" type="radio"/>
                <label for="round0">整数</label>
            </div>
            <div class="input-group">
                <input v-model="accuracy" id="round1" :value="1" name="round" type="radio"/>
                <label for="round1">一位小数</label>
            </div>
            <div class="input-group">
                <input v-model="accuracy" id="round2" :value="2" name="round" type="radio"/>
                <label for="round2">两位小数</label>
            </div>
            <div class="input-group">
                <input v-model="accuracy" id="roundNull" value="" name="round" type="radio"/>
                <label for="roundNull">不处理</label>
            </div>
        </div>
        <div class="equation-input mb-2">
            <input @keydown.enter="addResult" placeholder="请输入算式" v-model="equation"/>
            <div v-if="equation" class="btn-clear btn" @click="clearInput"><img src="./components/Button/icons/close.svg" alt="清空"></div>
        </div>
        <div class="tip-wrapper">
            <div class="clear-button" @click="clearHistory">清空列表</div>
            <div class="tip">{{ errTip }}</div>
        </div>
        <div class="calculator-container">

            <ResultList
                :resultList="resultList"
                @edit="editResultAt"
                @delete="deleteResultAt"
                @noteConfirm="noteConfirmAt"
                @note="noteResultAt"/>
            <Copyright/>
        </div>

    </div>
</template>

<script>

import Display from "@/components/Display";
import calculator from "advanced-calculator"
import ResultList from "@/components/ResultList";
import Button from "@/components/Button/Button";
import ClipboardJS from "clipboard";
import Copyright from "@/components/Copyright";

const RESULT_STORE_IDENTIFIER = 'CalculatorResultList'

export default {
    name: 'App',
    components: {Copyright, Button, ResultList, Display },
    data(){
        return {
            equation: '', // 算式
            result: '', // 计算结果,
            resultList: [], // 计算结果保存列表
            accuracy: 2, // 精度

            errTip: '', // 错误提示
        }
    },

    methods: {
        // 计算结果
        calculate(){
            this.equation = this.equation.replaceAll(/[xX]/g,'*')
            this.equation = this.equation.replaceAll(/[cC]/g,'/')
            this.equation = this.equation.replaceAll(/[jJ]/g,'+')
            this.equation = this.equation.replaceAll(/[\[（]/g,'(')
            this.equation = this.equation.replaceAll(/[\]）]/g,')')
            // console.log('---about to execute calculation: ', this.equation)
            try {
                if (this.equation !== ''){
                    let result = calculator.evaluate(this.equation)
                    // this.result = String(result)
                    if (this.accuracy !== ''){
                        this.result = Number(result.toFixed(this.accuracy))
                    } else {
                        this.result = result
                    }
                    this.errTip = ''
                }
            } catch (error) {
                console.log(error)
                this.result = ''
                this.errTip = '请检查算式'
            }
        },
        // 清空历史记录
        clearHistory(){
            this.resultList = []
        },
        // 添加结果到结果集
        addResult(){
            this.calculate()
            if (this.equation === ''){
                this.result = ''
            }
            if (this.equation && this.result){
                this.resultList.unshift({
                    date: new Date(),
                    // equation: this.equation.replaceAll(' ','').replaceAll(/([\+\-\(\)\/])/g, ' $1 '),
                    equation: this.equation.replaceAll(' ',''),
                    result: this.result,
                    isEditing: false,
                    note: '备注'
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
        noteResultAt(index){
            let editResult = this.resultList[index]
            editResult.isEditing = true
        },
        noteConfirmAt(index){
            let editResult = this.resultList[index]
            editResult.isEditing = false
        },
        clearInput(){
            this.equation = ''
        }
    },
    watch: {
        equation(newValue){
        },
        resultList: {
            deep: true,
            handler(newValue){
                localStorage.setItem(RESULT_STORE_IDENTIFIER, JSON.stringify(this.resultList))
            }
        }
    },

    mounted() {
        // 读取保存的数据
        let lastResultListString = localStorage.getItem(RESULT_STORE_IDENTIFIER)
        if (lastResultListString){
            this.resultList = JSON.parse(lastResultListString)
        } else {
            this.resultList = []
        }

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

<style lang="scss">
@import "assets/scss/calculator";


.container{
    font-family: 'Verdana';
    padding: 30px;
}

.equation-input{
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-flow: row nowrap;
    input{
        font-family: 'Verdana';
        width: 100%;
        display: block;
        text-align: center;
        font-size: 30px;
        padding: 10px 20px;
        border: 2px solid $color-border;
        @include border-radius(5px);
        outline: none;
        background-color: #fafafa;
        @include transition(all 0.3s);
        &:focus{
            outline: 4px solid transparentize($blue, 0.9);
            @include transition(all 0.3s);
            border: 2px solid transparentize($blue, 0.3);
            background-color: transparentize($blue, 0.98);
        }
    }
    .btn-clear{
        position: absolute;
        right: 30px;
        top: 15px;
        &:hover{
            background-color: transparentize($red, 0.6);
        }
    }
}

.calculator-container{
    display: flex;
    flex-flow: row nowrap;
}


.tip-wrapper{
    padding: 10px;
    display: flex;
    width: 100%;
    justify-content: center;
    align-content: center;
    flex-flow: column nowrap;
    text-align: center;
    .clear-button{
        text-align: center;
        cursor: pointer;
        font-size: $font-size-text;
        color: $color-subtitle;
        &:hover{
            color: $color-main;
        }
    }
    .tip{
        font-size: $font-size-text;
        color: $color-main;
    }
}

.input-group-list{
    align-items: center;
    margin-bottom: 10px;
    display: flex;
    justify-content: flex-start;
    .input-group{
        margin-right: 10px;
    }
}

</style>
