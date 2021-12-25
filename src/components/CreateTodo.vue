<template>
    <div>
        <form action="" class="todo" @submit.prevent="addTodo()">
            <input type="text" class="todo__input" placeholder="Create a new todo..." maxlength="30"  v-model="newTodo" />
            <button class="todo__ghostButton"></button>

            <div class="todo__content">
                <div class="todo__items">
                </div>
                <div class="todo__options">
                    <p class="todo__left">0 items left</p>
                    <p class="todo__clear">Clear Completed</p>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                newTodo: ""
            };
        },
        methods: {
            addTodo() {
                if (this.newTodo.length > 0) {
                    this.$emit("on-new-todo", this.newTodo);
                }
                this.newTodo = "";
            }
        }
    };
</script>

<style scoped>
</style>