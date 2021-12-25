<template>
  <li class="d-flex align-items-center list-group-item" style="
    list-style: none;
">
      <input name="" type="checkbox" value="" class="radio_prod" v-model="checkedTask" />
    <button
      class="btn border-0 flex-grow-1 text-left shadow-none"
      :class="{ completed }"
      @click="$emit('on-toggle')"
      v-if="!isEditing"
    >
      <span>{{ description }}</span>
    </button>
    <form v-else class="flex-grow-1" @submit.prevent="finishEditing()">
      <input
        type="text"
        class="form-control"
        v-model="newTodoDescription"
        @blur="finishEditing()"
        ref="newTodo"
      />
    </form>
    <button
      @click="startEditing()"
      class="btn btn-outline-primary border-0 ml-2"
    >edit
      <span class="fa fa-edit"></span>
    </button>
    <button @click="$emit('on-delete')" class="btn btn-outline-danger border-0">
    delete</button>
    <svg
          @click="$emit('on-delete')"
          class="absolute top-5 right-5 fill-current text-black cursor-pointer"
          fill="black"
          width="15"
          height="15"
          xmlns="http://www.w3.org/2000/svg"
        ></svg>
    <button>
        <span v-for="text in checkedTask" :key="text" :text="text" @tag="$emit('on-toggle', text)">{{text}}</span> 
    </button>
  </li>
</template>

<script>
export default {
  data() {
    return {
      isEditing: false,
      newTodoDescription: "",
      checkedTask: [],
    };
  },
  props: {
    description: Array,
    completed: Boolean
  },
  methods: {
    startEditing() {
      if (this.isEditing) {
        this.finishEditing();
      } else {
        this.newTodoDescription = this.description;
        this.isEditing = true;
        this.$nextTick(() => this.$refs.newTodo.focus());
      }
    },
    finishEditing() {
      this.isEditing = false;
      this.$emit("on-edit", this.newTodoDescription);
    },
    CompletedTask() {
        this.isCompleted = false;
        this.$emit("on-toggle", this.checkedTask);
    }
  },
  computed: {
    getTasks () {
        console.log(this.description.checkedTask)
      return [this.description.checkedTask]
    },

  }
};
</script>

<style lang="scss" scoped>
.completed {
  text-decoration: line-through;
}
</style>
