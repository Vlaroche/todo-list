<template>
    <li  class="bg-white p-2 rounded mt-1 border-b border-grey cursor-pointer hover:bg-grey-lighter" >
        <input class="m-2" type="checkbox" :value="!item.isEnded" v-model="item.isEnded">
        <span :class="isEndedStyle">{{ item.content }}</span>
        <span @click="$emit('removeItem', item.id)" class="deleteIcon"> - </span>
    </li>
</template>

<script>
    export default {
        name: 'Item',
        props: {
            itemProps: Object
        },
        data() {
            return {
                item : this.itemProps
            }
        },
        watch: {
            item: {
                handler(newItem) {
                    this.$emit('editItem', newItem)
                },
                deep: true
            }
        },
        computed: {
            isEndedStyle() {
                return {
                    ended : this.item.isEnded
                }
            },
        },
        emits: ['removeItem', 'editItem']
    }
</script>

<style scoped>
    .ended {
        text-decoration: line-through;
    }
    .deleteIcon{
        background-color:#de3f53;
        border-radius:50%;
        color:#fff;
        float:right;
        font-weight: bold;
        line-height: normal;
        height:20px;
        margin-top: 5px;
        text-align: center;
        text-decoration: none;
        width:16px;
        -webkit-transition: all .2s linear;
        -moz-transition: all .2s linear;
        -o-transition: all .2s linear;
        transition: all .2s linear; 
    }
</style>