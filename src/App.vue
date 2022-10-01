<template>
  <div class="app">
    <h1>Задачи</h1>
    <my-button @click="showDialog" style="margin: 15px 0"
      >Создать задачу</my-button
    >
    <my-dialog v-model:show="dialogVisible">
      <task-form
        @create="createTask"
        @closeDialog="closeDialogWindow"
      ></task-form>
    </my-dialog>
    <task-list
      :tasks="tasks"
      @remove="removeTask"
      @ready="taskReady"
    ></task-list>
  </div>
</template>

<script>
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import MyDialog from "./components/UI/MyDialog.vue";

export default {
  components: {
    TaskForm,
    TaskList,
    MyDialog,
  },
  data() {
    return {
      tasks: [
        {
          title: "Сделать приложение",
          description:
            "Сделай нормальное приложение, через три месяца надо уже прогером нормальным быть",
          id: 1,
          status: false,
        },
      ],
      dialogVisible: false,
    };
  },
  methods: {
    createTask(task) {
      this.tasks.push(task);
    },
    removeTask(task) {
      this.tasks = this.tasks.filter((t) => t.id !== task.id);
    },
    showDialog() {
      this.dialogVisible = true;
    },
    closeDialogWindow() {
      this.dialogVisible = false;
    },
  },
};
</script>

<style scoped>
.app {
  padding: 20px;
}
</style>