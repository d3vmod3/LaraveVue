<template>
        <div class="todoListContainer">
            <div class="heading">
                <h2 id="title">Todo List</h2>
                <add-item-form 
                v-on:reloadlist="getList()"
                />
            </div>
            <list-view 
                :items="items"
                v-on:reloadlist="getList()"
            />
        </div>
        
</template>

<script>
import Axios from "axios"
import addItemForm from "./addItemForm"
import listView from "./listView"

export default{
    components:{
        addItemForm,
        listView
    },
    data: function () {
        return {
            items: []
        }
    },
    methods:{
        getList () {
            Axios.get('api/items')
            .then( response =>{
                this.items = response.data
            })
            .catch (error => {
                console.log( error );
            })
        }
    },
    created (){
        this.getList();
    }
}
</script>

<style>
.todoListContainer{
    width: 400px;
    margin:auto;
}

.heading{
    background-color: #e6e6e6;
    padding: 10px;
}

#title{
    text-align:center;
}
</style>