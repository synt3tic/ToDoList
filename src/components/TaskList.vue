<template>
  <div v-if="tasks.length > 0">
    <h3>Список задач</h3>
    <task-item
      class="task"
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @remove="$emit('remove', task)"
      @statusChange="isTaskReady"
      @edit="editTask"
    />
  </div>
  <h3 v-else>Список задач пуст</h3>
</template>

<script>
import TaskItem from "./TaskItem.vue";
export default {
  components: { TaskItem },
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
  methods: {
    isTaskReady(id) {
      this.tasks.map((el) => {
        if (el.id === id) {
          el.status = !el.status;
        }
      });
    },
    editTask(taskId) {
      this.tasks.map((el) => {
        if (el.id === taskId) {
          console.log(this.editStatus);
        }
      });
    },
  },
};
</script>

<style scoped>
.task {
  border: 2px solid teal;
  margin-top: 10px;
  padding: 15px;
  border-radius: 10px;
}
</style>