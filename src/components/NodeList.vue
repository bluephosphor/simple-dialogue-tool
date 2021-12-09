<script>
import DialogueNode from './DialogueNode'

export default {
    components: {
        DialogueNode
    },
    props: {
        nodes: Array
    }
}
</script>

<template>
    <DialogueNode 
        class="dialogue-node"
        v-for="(node, index) in nodes" 
        :key="index"
        :nodeData="node"
    />
</template>