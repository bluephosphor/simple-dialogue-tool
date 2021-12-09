<template>
    <button 
        @click="onClick()" 
        :style="`background: ${color}`"
        class="btn">
        {{ text }}
    </button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text: String,
        color: String,
    },
    methods:{
        onClick(){
            this.$emit('btn-click')
        }
    }
}
</script>

<style scoped>
    .btn{
        color: white;
        background: black;
        border: 1px solid white;
        border-radius: 4px;
        font-size: 0.7em;
        padding: 4px 8px;
    }
</style>