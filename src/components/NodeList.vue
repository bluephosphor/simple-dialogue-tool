<script>
import DialogueNode from './DialogueNode'

export default {
    components: {
        DialogueNode
    },
    data(){
        return {
            nodes: [
                {
                    id: 0, 
                    text: 'This is a test.'
                },
                {
                    id: 1, 
                    text: 'This is another test.'
                },
                {
                    id: 2, 
                    text: 'Hello. This is yet another test.'
                },
                {
                    id: 3, 
                    text: 'Aaand, this is the last test.'
                },
            ]
        }
    }
}
</script>

<template>
    <DialogueNode 
        class="dialogue-node"
        v-for="node in nodes" 
        :key="node.id"
        :nodeData="node"
    />
</template>

<style scoped>
    .dialogue-node {
        margin: 5px;
    }
</style>