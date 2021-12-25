<template>
    <div>
        <div class="row mb-3">
            <CreateTodo @on-new-todo="addTodo($event)" />
        </div>
        <div class="row">
            <div class="col-12 col-sm-10 col-lg-6">
                <ul class="list-group">
                    <todo v-for="(todo, index) in todos" :key="index" :description="todo.description"
                        :completed="todo.completed" @on-toggle="toggleTodo(todo)" @on-delete="deleteTodo(todo)"
                        @on-edit="editTodo(todo, $event)" />
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    import Todo from "./Todo.vue";
    import CreateTodo from "./CreateTodo.vue";
    export default {
        components: {
            CreateTodo,
            Todo
        },
        data() {
            return {
                todos: [{
                        description: "Jog around the park 3x",
                        completed: false
                    },
                    {
                        description: "10 minutes meditation",
                        completed: false
                    },
                    {
                        description: "Read for 1 hour",
                        completed: false
                    },
                    {
                        description: "Pick up groceries",
                        completed: false
                    },
                    {
                        description: "Complete Todo app on Frontend Mentor",
                        completed: false
                    },
                ],
                done: [{
                    description: "",
                    completed: true
                }]
            };
        },
        methods: {
    addTodo(newTodo) {
      this.todos.push({ description: newTodo, completed: false });
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter(todo => todo !== deletedTodo);
    },
    editTodo(todo, newTodoDescription) {
      todo.description = newTodoDescription;
    },
    doneTask(todo) {
        this.todos.push({description: todo, completed: true})
    }
  },
    }
</script>

<style scoped>

</style>