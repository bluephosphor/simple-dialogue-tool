<template>
    <button 
        @click="onClick()" 
        :class="`btn btn-outline-${theme} btn-small`">
        {{ text }}
    </button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text: String,
        theme: String,
    },
    methods:{
        onClick(){
            this.$emit('btn-click')
        }
    }
}
</script>