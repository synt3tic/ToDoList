<template>
  <div class="task">
    <div v-if="!task.editStatus">
      <div :class="{ task__ready: task.status }">
        <strong>Название:</strong> {{ task.title }}
      </div>
      <div :class="{ task__ready: task.status }">
        <strong>Описание:</strong> {{ task.body }}
      </div>
    </div>
    <div v-else>
      <div :class="{ task__ready: task.status }">
        <strong>Название:</strong>
        <my-input type="text" v-model="task.title" />
      </div>
      <div :class="{ task__ready: task.status }">
        <strong>Описание:</strong>
        <my-input class="input" type="text" v-model="task.body" />
      </div>
      <my-button @click="editTask">Сохранить изменения</my-button>
    </div>
    <div class="btns">
      <my-button class="task__btn" @click="$emit('ready', task.id)"
        >Выполнена</my-button
      >
      <my-button
        v-show="!task.status"
        class="task__btn"
        @click="$emit('edit', task.id)"
        >Редактировать</my-button
      >
      <my-button class="task__btn" @click="$emit('remove', task)"
        >Удалить</my-button
      >
      <div v-show="task.status" style="color: teal">Выполнена ✓</div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    editStatus: false,
  }),
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  methods: {
    editTask() {
      this.task.editStatus = false;
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

.task__ready {
  text-decoration: line-through;
  color: gray;
}

.input {
  width: 95%;
  height: 5px;
}
</style>