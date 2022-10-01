<template>
  <form class="form" @submit.prevent>
    <my-input v-model="task.title" type="text" placeholder="Название задачи" />
    <my-input
      v-model="task.description"
      type="text"
      placeholder="Описание задачи"
    />
    <my-button class="btn btn_form" @click="createTask"
      >Создать задачу</my-button
    >
  </form>
</template>

<script>
import MyInput from "./UI/MyInput.vue";
export default {
  components: { MyInput },
  data() {
    return {
      task: {
        title: "",
        description: "",
      },
    };
  },
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    createTask() {
      this.task.id = Date.now();
      this.task.status = false;
      this.$emit("create", this.task);
      this.task = {
        title: "",
        body: "",
      };
      this.$emit("closeDialog", false);
    },
  },
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
}

.btn_form {
  align-self: flex-end;
}
</style>