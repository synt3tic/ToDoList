<template>
  <div class="task">
    <div v-if="!editStatus">
      <div :class="{ task_ready: task.status }">
        <strong>Название:</strong> {{ task.title }}
      </div>
      <div :class="{ task_ready: task.status }">
        <strong>Описание:</strong> {{ task.description }}
      </div>
    </div>
    <div v-else>
      <div :class="{ task_ready: task.status }">
        <strong>Название:</strong>
        <my-input type="text" v-model="task.title" />
      </div>
      <div :class="{ task_ready: task.status }">
        <strong>Описание:</strong>
        <my-input class="input" type="text" v-model="task.description" />
      </div>
    </div>
    <div class="btns">
      <my-button class="task__btn" @click="$emit('statusChange', task.id)">{{
        taskStatusButton
      }}</my-button>
      <my-button v-show="!task.status" class="task__btn" @click="editTask">{{
        editStatusValue
      }}</my-button>
      <my-button class="task__btn" @click="$emit('remove', task)"
        >Удалить</my-button
      >
      <div style="color: teal">{{ taskStatus }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      editStatus: false,
    };
  },
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  methods: {
    editTask() {
      this.editStatus = !this.editStatus;
    },
  },
  computed: {
    taskStatus: function () {
      if (this.task.status) {
        return "Выполнена ✓";
      } else {
        return "В процессе ◉";
      }
    },
    taskStatusButton: function () {
      if (this.task.status) {
        return "Не выполнена";
      } else {
        return "Выполнена";
      }
    },
    editStatusValue: function () {
      if (this.editStatus) {
        return "Сохранить изменения";
      } else {
        return "Редактировать";
      }
    },
  },
};
</script>

<style scoped>
.btns {
  display: flex;
  align-items: center;
  margin-top: 10px;
}

.task__btn {
  margin: 3px;
}

.task_ready {
  text-decoration: line-through;
  color: gray;
}

.input {
  width: 95%;
  height: 5px;
}
</style>