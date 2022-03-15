<template>
    <ResultListItem :resultItem="item"
                    v-for="(item, index) in resultList" :key="index"
                    @delete="$emit('delete', )"
    />
</template>

<script>
import ResultListItem from "@/components/ResultListItem";
export default {
    name: "ResultList",
    components: {ResultListItem},
    props: {
        resultList: []
    },
    methods: {
    }
}
</script>

<style lang="scss" scoped>
@import "src/assets/scss/plugin";

</style>
