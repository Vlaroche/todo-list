<template>
    <div class='w-3/6 rounded shadow p-2 bg-green-200 flex flex-col'>
        <h1>To Do List</h1>
        <ul>
            <Item v-for="item in todoListItem" :key="item.id" :itemProps="item" @removeItem="removeItem" @editItem="editItem"/>
        </ul>
        <input class="rounded m-2 flex p-2" v-on:keyup.enter="submitItem" type="text" placeholder="Add some text and press Enter" v-model="formContent">
    </div>
</template>

<script>
    import Item from './Item.vue'

    export default {
        name: 'TodoList',
        components: {
            Item
        },
        mounted() {
            if (localStorage.getItem('todoListItem')) {
                try {
                    this.todoListItem = JSON.parse(localStorage.getItem('todoListItem'));
                } catch(e) {
                    localStorage.removeItem('todoListItem');
                }
            }
        },
        data() {
            return {
                todoListItem : [
                ],
                formContent: "",
            }
        },
        methods: {
            submitItem() {
                let currentId = this.todoListItem.length > 0 ? this.todoListItem[this.todoListItem.length - 1].id + 1 : 0;
                this.todoListItem.push({
                    id: currentId,
                    content: this.formContent,
                    isEnded: false
                });
                this.formContent = ""
                this.saveItems();
            },
            removeItem(removeId) { 
                let index = this.todoListItem.findIndex(element => element.id == removeId);
                this.todoListItem.splice(index, 1);
                this.saveItems();
            },
            editItem(editedIem) { 
                let index = this.todoListItem.findIndex(element => element.id == editedIem.id);
                this.todoListItem.splice(index, 1, editedIem);
                this.saveItems();
            },
            saveItems() {
                localStorage.setItem('todoListItem', JSON.stringify(this.todoListItem));
            }
        }
    }
</script>

<style scoped>
</style>