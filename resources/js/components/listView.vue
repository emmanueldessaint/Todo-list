<template>
    <div>
        <add-item-form v-on:reloadTodos="getTodos()"/>
        <div v-for="(item, index) in items" :key="index">
            <list-item
            :item="item"           
            v-on:reloadTodos="getTodos()"
            
            class="item"
            />
        </div>
    </div>
</template>

<script>
import listItem from './listItem'
import addItemForm from './addItemForm'

export default {
    components: {
        listItem,
        addItemForm
        
    },
    data: function() {
        return {
            items: []
        }
    },
    methods: {
        getTodos() {
            axios.get('api/todos').then(response => {
                if(response.status === 200) {
                    console.log(response.data.todos)
                    this.items = response.data.todos
                }
            })
        }
    },
    created() {
        this.getTodos()
    }
}
</script>

<style>
.item {
    padding:12px;
    margin-top:5px;
    border-style:solid;
    border-color:blue;
    border-radius:7px;
    border-width:1px;
}
</style>