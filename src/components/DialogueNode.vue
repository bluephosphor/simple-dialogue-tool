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
    <div class="card" style="width: 40%">
        <img src="" class="card-img-top" alt="">
        <div class="card-body">
            <p class="card-title">id: {{this.nodeData.id}}</p>
            <div v-if="this.editing" class="form-group mt-4 mb-2">
                <input
                    v-model="this.text"
                    class="form-control form-control-sm"
                    placeholder="text"
                />
            </div>
            <p v-else class="card-text">{{this.text}}</p>
            <Button :text="this.editing ? 'Save' : 'Edit'" theme="primary" @click="toggleEdit" />
        </div>
    </div>
</template>

<style scoped>
    .form-control,
    .card-text{
        font-family: monospace
    }
</style>