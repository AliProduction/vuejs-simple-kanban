<template>
  <div class="container p-8 mx-auto">
    <input
      v-model="newTask"
      class="
        w-full
        px-3
        py-2
        leading-tight
        text-gray-700
        border
        rounded
        shadow
        appearance-none
        focus:outline-none focus:shadow-outline
      "
      type="text"
      placeholder="New Task"
    />

    <input
      v-model="finishDate"
      class="
        w-full
        mt-3
        px-3
        py-2
        leading-tight
        text-gray-700
        border
        rounded
        shadow
        appearance-none
        focus:outline-none focus:shadow-outline
      "
      type="date"
      placeholder="ikul"
    />

    <button
      class="
        bg-blue-500
        hover:bg-blue-700
        text-white
        font-bold
        mt-3
        py-2
        px-4
        rounded
      "
      @click="createNewTask"
    >
      Create Task
    </button>

    <div class="grid grid-cols-3 mt-4">
      <div class="px-3 py-3 mr-4 bg-gray-100 rounded-lg">
        <p class="text-sm font-semibold tracking-wide text-gray-700">To Do</p>
        <KanbanColumn
          :list="todo"
          @click-close="removeTask(...arguments, todo)"
        />
      </div>

      <div class="px-3 py-3 mr-4 bg-gray-100 rounded-lg">
        <p class="text-sm font-semibold tracking-wide text-gray-700">Doing</p>
        <KanbanColumn
          :list="doing"
          @click-close="removeTask(...arguments, doing)"
        />
      </div>

      <div class="px-3 py-3 mr-4 bg-gray-100 rounded-lg">
        <p class="text-sm font-semibold tracking-wide text-gray-700">Done</p>
        <KanbanColumn
          :list="done"
          @click-close="removeTask(...arguments, done)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import KanbanColumn from './components/KanbanColumn.vue';

export default {
  components: { KanbanColumn },
  data: {
    newTask: '',
    finishDate: '',
  },
  data() {
    return {
      todo: [],
      doing: [],
      done: [],
    };
  },
  methods: {
    formatDate(input) {
      var datePart = input.match(/\d+/g),
        year = datePart[0],
        month = datePart[1],
        day = datePart[2];

      return day + '.' + month + '.' + year;
    },

    removeTask(task, list) {
      const i = list.indexOf(task);
      if (i > -1) {
        list.splice(i, 1);
      }
    },

    createNewTask() {
      if (this.newTask.length !== 0) {
        this.todo.push({
          name: this.newTask,
          finishDate: this.formatDate(this.finishDate),
        });
        this.newTask = '';
      }
    },
  },
};
</script>
