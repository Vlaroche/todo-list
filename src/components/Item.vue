<template>
    <li  class="list">
        <!-- <input type="checkbox" :value="!item.isEnded" v-model="item.isEnded" @click="$emit('editItem', item)"> -->
        <input type="checkbox" :value="!item.isEnded" v-model="item.isEnded">
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
    .list{
        flex: 1 auto;
        text-align: center;
        list-style-type: none;
    }
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
        height:16px;
        margin-top: 20px;
        text-align: center;
        text-decoration: none;
        width:16px;
        -webkit-transition: all .2s linear;
        -moz-transition: all .2s linear;
        -o-transition: all .2s linear;
        transition: all .2s linear; 
    }
</style>