<template>
    <div class="addItem">
        <input type="text" v-model="item.name"/>
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[ item.name ? 'active' : 'inactive', 'plus' ]"
        />
    </div>
</template>
<script>
import Axios from 'axios';

export default{
    data: function (){
        return{
            item:{
                name: ""
            }
        }
    },
    methods:{
        addItem(){
            if( this.item.name == '' ){
                return;
            }

            Axios.post('api/item/store', {
                item: this.item
            })
            .then( response =>{
                if(response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch ( error =>{
                console.log(error);
            })
        }
    }
}
</script>


<style>

.AddItem{
    display: fixed;
    justify-content: center;
    align-items: center;
}

input{
    background-color: #f7f7f7;
    border: 0px;
    outline: none;
    margin-right: 10px;
    width: 100%;
}

.plus{
    font-size: 20px;
}
.active{
    color: #00ce25;
}
.iactive{
    color: #999999;
}


</style>