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
    <div class="card" style="width: 18rem;">
        <img src="" class="card-img-top" alt="">
        <div class="card-body">
            <h5 class="card-title">{{this.nodeData.id}}</h5>
            <div v-if="this.editing" class="form-group mt-4 mb-2">
                <input
                    v-model="this.text"
                    class="form-control form-control-sm"
                    placeholder="text"
                />
            </div>
            <p v-else class="card-text">{{this.text}}</p>
            <Button text="Edit" color="blue" @click="toggleEdit" />
        </div>
    </div>
</template>

<style scoped>
    .form-control,
    .card-text{
        font-family: monospace
    }
</style>