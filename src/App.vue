<template>
  <div class="todoapp">
    <TodoHeader @add="addFn" />
    <TodoMain :list="list" @del="delFn" />
    <TodoFooter />
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoMain from "./components/TodoMain.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  name: "App",
  data() {
    return {
      list: [
        { id: 100, name: "吃饭", isDone: true },
        { id: 101, name: "睡觉", isDone: false },
        { id: 102, name: "打豆豆", isDone: true },
      ],
    };
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    addFn(val) {
      this.list.unshift({
        id: this.list[0] ? this.list[this.list.length - 1].id + 1 : 100,
        name: val,
        isDone: false,
      });
    },
    delFn(id) {
      const index = this.list.findIndex((item) => item.id == id);
      this.list.splice(index, 1);
    },
  },
};
</script>

<style>
</style>