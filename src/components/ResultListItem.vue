<template>
    <div class="result-item">
        <div class="equation">{{resultItem.equation.replaceAll(/\*/g, '×').replaceAll(/\//g, '÷')}}</div>
        <div class="right">
            <div class="equal">=</div>
            <div class="result">{{resultItem.result}}</div>
            <div class="operations">
                <Button type="edit" @click="$emit('edit', index)"/>
                <Button type="close" @click="$emit('delete', index)"/>
                <Button type="share" class="clipboard"  :dataClipboard="resultItem.result"/>
            </div>
            <input v-if="resultItem.isEditing"
                   @keydown.enter="$emit('noteConfirm', index)"
                   v-model="resultItem.note" class="note-input" type="text">
            <div v-else
                 class="note"
                 @click="$emit('note', index)"
            >{{resultItem.note || ''}}</div>
        </div>
    </div>
</template>

<script>
import Button from "@/components/Button/Button";
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
    emits: ['delete', 'edit', 'note', 'noteConfirm'],
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
        align-items: center;
        .equal{
            color: $blue;
            padding-right: 50px;
        }
        .result{
            //flex-grow: 1;
        }
        .note{
            padding: 5px 10px;
            font-size: $font-size-comment;
            color: $text-main;
            &:hover{
                font-weight: bold;
            }
        }
        .note-input{
            font-size: $font-size-comment;
            padding: 5px 10px;
            @include border-radius(3px);
            outline: none;
            border: 1px solid $color-border;
            &:focus{
                border-color: $color-border-highlight;
            }
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
