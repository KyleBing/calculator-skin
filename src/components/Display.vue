<template>
    <div class="display">
        <div class="equation">{{equation}}</div>
        <div class="equal">=</div>
        <div class="result">{{result}}</div>
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

.result{

}

.equal{
    color: $text-comment;
}

.equation{

}

</style>
