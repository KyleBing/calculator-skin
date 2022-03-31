<template>
    <div class="result-item">
        <div class="equation">{{resultItem.equation.replaceAll(/\*/g, '×').replaceAll(/\//g, '÷')}}</div>
        <div class="right">
            <div class="equal">=</div>
            <div class="result">{{resultItem.result}}</div>
            <div class="operations">
                <Button type="edit" @click="$emit('edit', index)"/>
                <Button type="delete" @click="$emit('delete', index)"/>
                <Button class="clipboard" type="share" :dataClipboard="resultItem.result"/>
            </div>
        </div>
    </div>
</template>

<script>
import Button from "@/components/Button/Button";
import ClipboardJS from "clipboard";
export default {
    name: "ResultListItem",
    components: {Button},
    props:{
        resultItem: {},
        index: {
            type: Number,
            required: true
        }
    },
    emits: ['delete', 'edit']
}
</script>

<style lang="scss" scoped>
@import "src/assets/scss/plugin";
.result-item{
    font-size: 30px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-flow: row nowrap;
    padding: 10px;
    &:hover{
        background-color: transparentize(black, 0.95);
    }
    .equation{
        padding-right: 50px;
        flex-grow: 1;
        text-align: right;
    }
    .right{
        width: 50%;
        flex-shrink: 0;
        display: flex;
        justify-content: flex-start;
        .equal{
            color: $blue;
            padding-right: 50px;
        }
        .result{

        }
    }
}



.operations{
    margin-left: 20px;
    align-items: center;
    display: flex;
    flex-flow: row nowrap;
    &> * {
        margin-right: 5px;
    }
}

</style>
