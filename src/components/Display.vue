<template>
    <div class="display">
        <div class="equation">{{equation}}</div>
        <div class="right">
            <div class="equal">=</div>
            <div class="result">{{result}}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Display",
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

.display{
    flex-flow: row nowrap;
    align-items: center;
    display: flex;
    justify-content: center;
    font-size: 40px;
    font-weight: bold;
    text-align: center;
    color: $text-main;
}

.equation{
    text-align: right;
    flex-grow: 1;
    padding-right: 50px;
}
.right{
    width: 50%;
    flex-shrink: 0;
    display: flex;
    .equal{
        padding-right: 50px;
        color: $text-comment;
    }
    .result{
    }
}


</style>
