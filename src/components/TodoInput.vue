<template>
    <div class="inputBox shadow">
        <input type="text" class="textBox" v-model="newTodoItem" placeholder="write here" v-on:keyup.enter="addTodo">
        <span class="addContainer2" v-on:click="removeInput">
            <i class="fa-solid fa-trash" aria-hidden="true"></i>
        </span>
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fa fa-plus" aria-hidden="true"></i>
        </span>

        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">경고</h3>
            <h4 slot="body">할 일을 입력하세요.</h4>
            <span slot="footer" @click="showModal = false">
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i> 
            </span>
        </modal>
    </div>
</template>


<script>

    import Modal from './common/Modal.vue'


    export default {
        data(){
            return{
                newTodoItem: '',
                showModal:false
            }
        },
        methods: {
            addTodo(){
                if(this.newTodoItem !== ""){
                    var value = this.newTodoItem && this.newTodoItem.trim();
                    this.$emit('addTodo', value);
                    this.clearInput();
                } else {
                    this.showModal = !this.showModal;
                }
                
            },
            clearInput(){
                this.newTodoItem ='';
            },
            removeInput(){
                var el = document.getElementsByClassName('textBox');
                for(var i=0; i<el.length; i++){	el[i].value = '';}
            }
        },
        components: {
            Modal : Modal
        }
    }
    
</script>

<style >
    input:focus {
        outline: none;
    }
    .inputBox{
        background-color: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input {
        border-style:none;
        font-size: 0.9rem;
        width: 80%;
        height: inherit;
        text-align: center;
    }
    .addContainer{
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 1.5rem;
        border-radius: 5px;
        cursor: pointer;
    }
    .addContainer2{
        color: white;
        float: right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 1.5rem;
        border-radius: 5px;
        cursor: pointer;
    }
    .addBtn{
        color: wheat;
        vertical-align: middle;
        cursor: pointer;
    }
</style>