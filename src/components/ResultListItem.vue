<template>
    <div class="result-item">
        <div class="equation">{{resultItem.equation}}</div>
        <div class="equal">=</div>
        <div class="result">{{resultItem.result}}</div>
        <div class="operations">
<!--            <div class="operation-item">+</div>-->
            <div class="operation-item" @click="$emit('delete', resultItem)">-</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ResultListItem",
    props:{
        resultItem: {

        }
    }
}
</script>

<style lang="scss" scoped>
@import "src/assets/scss/plugin";
.result-item{
    font-size: 30px;
    display: flex;
    justify-content: center;
    flex-flow: row nowrap;
}

.operations{
    display: flex;
    flex-flow: row nowrap;
    .operation-item{
        padding: 2px 5px;
        line-height: 1;
        border: 1px solid $color-border;
        @include border-radius(5px);
        @extend .btn-like
    }
}

</style>
