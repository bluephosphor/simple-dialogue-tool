<script>
import Button from './Button';

export default {
    name: 'DialogueNode',
    components: {
        Button,
    },
    props: {
        nodeData: Object
    },
    data(){
        return {
            editing: false,
            text: this.nodeData.text
        }
    },
    methods: {
        toggleEdit(){
            this.editing = !this.editing;
        }
    }
}
</script>

<template>
    <div class="card">
        <div class="card-body">
            <p class="label"> Text: </p>
            <input 
                v-if="this.editing"
                v-model="this.text"
                class="text-input"
                placeholder="text"
            />
            <p v-else class="card-text">{{this.text}}</p>
        </div>
        <Button :text="this.editing ? 'Save' : 'Edit'" color="blue" @click="toggleEdit" />
    </div>
</template>

<style scoped>
    .card{
        width: 40%;
        border: 1px solid gray;
        border-radius: 5px;
        font-family: monospace;
        margin:16px 8px;
        padding: 8px;
    }

    .card-body{
        display: flex;
        
    }

    .label{
        margin-right: 8px;
    }

    .text-input{
        font-family: monospace;
        background: black;
        color: white;
        border: 1px solid white;
        padding: 4px;
        margin: 8px 0px;
        width: 80%
    }
</style>