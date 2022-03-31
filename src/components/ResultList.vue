<template>
    <ResultListItem :resultItem="item"
                    :index="index"
                    v-for="(item, index) in resultList" :key="index"
                    @delete="deleteResultAt(index)"
    />
</template>

<script>
import ResultListItem from "@/components/ResultListItem";
export default {
    name: "ResultList",
    components: {ResultListItem},
    props: {
        resultList: {
            type: Array,
            default: []
        }
    },
    emits: ['delete', 'edit'],
    methods: {
        deleteResultAt(index){
            this.$emit('delete', index)
        }
    }
}
</script>

<style lang="scss" scoped>
@import "src/assets/scss/plugin";

</style>
