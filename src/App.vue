<template>
  <div>
    <h1>TaskList</h1>
    <button @click="handleShowHideList">Ver a lista</button>
    <br />

    <input
      type="text"
      v-model="state.currentTask"
      placeholder="Digite sua task"
      @keyup.enter="addTask"
      v-focus
    />

    <ul v-if="state.showList">
      <li
        v-for="(task, index) in state.tasks"
        @dblclick="complete(task)"
        class="task-item"
        :key="`${task}-${index}`"
        :class="{ 'line-through': task.isDone }"
      >
        {{ task.name }} <button @click="remove(task)">&times;</button>
      </li>
    </ul>
    <p v-else>Lista de tafefas escondida.</p>
  </div>
</template>

<script>
import { reactive } from "vue";

const focus = {
  inserted: (el) => {
    el.focus();
  },
};

export default {
  directives: {
    focus,
  },
  setup() {
    const state = reactive({
      showList: false,
      currentTask: "",
      tasks: [
        { name: "Comprar leche", isDone: false },
        { name: "Comprar pan", isDone: false },
        { name: "Comprar huevos", isDone: false },
        { name: "Comprar carne", isDone: false },
      ],
    });

    function remove(task) {
      state.tasks = state.tasks.filter((t) => t.name !== task.name);
    }

    function complete(task) {
      state.tasks = state.tasks.map((t) => {
        if (t.name === task.name) {
          return { ...t, isDone: !t.isDone };
        }
        return { ...t };
      });
    }

    function handleShowHideList() {
      state.showList = !state.showList;
    }
    
    function addTask() {
      state.tasks.push({ name: state.currentTask, isDone: false });
      state.currentTask = "";
    }

    return { state, remove, complete, handleShowHideList, addTask };
  },
};
</script>
<style scoped>
.line-through {
  text-decoration: line-through;
}
.task-item {
  cursor: pointer;
}
</style>