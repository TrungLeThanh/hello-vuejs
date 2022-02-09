<template>
  <div id="id">
    <h1>Hello Vue</h1>
    <div>
      <input type="text" v-model="task_new" @keyup.enter="onEnter" />
      <button @click="addTask()">Add</button>
      <div class="wrap-task" v-for="item in tasks" :key="item.id">
        <input type="checkbox" v-model="item.status" />
        <p :class="{ done: item.status }">{{ item.name }}</p>
        <button @click="deleteTask(item.id)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      task_new: "",
      tasks: [],
    };
  },
  components: {},

  methods: {
    addTask: function () {
      this.tasks.push({ name: this.task_new, state: false });
    },

    onEnter: function () {
      this.tasks.push({ id: Math.random(), name: this.task_new, state: false });
    },

    deleteTask: function (id) {
      this.tasks = this.tasks.filter((item) => item.id !== id);
    },
  },

  watch: {
    tasks: function () {
      this.task_new = "";
    },
  },
};
</script>

<style>
.wrap-task {
  display: flex;
  align-items: center;
  gap: 15px;
}

.done {
  text-decoration: line-through;
}
</style>
