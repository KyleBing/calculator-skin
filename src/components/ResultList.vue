<template>
    <div class="result-list">
        <ResultListItem :resultItem="item"
                        :index="index"
                        v-for="(item, index) in resultList" :key="index"
                        @delete="deleteResultAt(index)"
                        @edit="editResultAt(index)"
                        @note="noteResultAt(index)"
                        @noteConfirm="noteConfirmAt(index)"
        />
    </div>
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
    emits: ['delete', 'edit', 'note', 'noteConfirm'],
    methods: {
        deleteResultAt(index){
            this.$emit('delete', index)
        },
        editResultAt(index){
            this.$emit('edit', index)
        },
        noteResultAt(index){
            this.$emit('note', index)
        },
        noteConfirmAt(index){
            this.$emit('noteConfirm', index)
        }
    }
}
</script>

<style lang="scss" scoped>
@import "src/assets/scss/plugin";
.result-list{
    margin-top: 20px;
    flex-shrink: 0;
    flex-grow: 1;
}

</style>
