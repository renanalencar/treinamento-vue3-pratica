<template>
  <div>
    <h1>Minha lista de tarefas!</h1>
    <button @click="handleShowHideList()">Ver a lista!</button>
    <br />
    <input type="text" @keyup.enter="addTask" v-model="currentTask" />

    <ul v-if="showList">
      <li
        v-for="(task, index) in tasks"
        :key="`${task}-${index}`"
        @dblclick="complete(task)"
        class="task-item"
        :class="{ 'line-through': task.isDone }"
      >
        {{ task.name }}
        <button @click="remove(task)">&times;</button>
      </li>
    </ul>
    <p v-else>Lista de tarefas escondida</p>
  </div>
</template>

<script>
const focus = {
  inserted: (el) => {
    el.focus();
  },
};
export default {
  directives: {
    focus,
  },
  data: () => ({
    currentTask: "",
    showList: false,
    tasks: [{ name: "Fazer curso", isDone: false }],
  }),
  methods: {
    addTask() {
      this.tasks.push({ name: this.currentTask, isDone: false });
      this.currentTask = "";
    },
    complete(task) {
      this.tasks = this.tasks.map((t) => {
        if (t.name === task.name) {
          return { ...t, isDone: !t.isDone };
        }
      });
    },
    handleShowHideList() {
      this.showList = !this.showList;
    },
    remove(task) {
      this.tasks = this.tasks.filter((t) => t.name !== task.name);
      // console.log('task', task)
    },
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