<template>
  <div class="todoapp">
    <TodoHeader @add="addFn" @isAll="isChecked" />
    <TodoMain :list="exhibition" @del="delFn" />
    <TodoFooter :listSum="listSum" @upData="upDataFn" @clear="clearFn" />
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
      list: JSON.parse(localStorage.getItem("list")) || [],
      val: "all",
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
        id: this.list[0] ? this.list[0].id + 1 : 100,
        name: val,
        isDone: false,
      });
    },
    delFn(id) {
      const index = this.list.findIndex((item) => item.id == id);
      this.list.splice(index, 1);
    },
    upDataFn(val) {
      this.val = val;
    },
    clearFn() {
      this.list = this.list.filter((item) => !item.isDone);
    },
    isChecked(val) {
      this.list.forEach((item) => (item.isDone = val));
    },
  },
  computed: {
    listSum() {
      return this.list.filter((item) => !item.isDone).length;
    },
    exhibition() {
      if (this.val == "all") {
        return this.list;
      } else if (this.val == "ok") {
        return this.list.filter((item) => item.isDone);
      } else {
        return this.list.filter((item) => !item.isDone);
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler(val) {
        localStorage.setItem("list", JSON.stringify(val || []));
      },
    },
  },
};
</script>

<style>
</style>