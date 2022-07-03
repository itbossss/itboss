<template>
  <div class="todoapp">
    <TodoHeader @add="addFn"></TodoHeader>
    <TodoMain :list="showList" @delFn="delFnn"></TodoMain>
    <TodoFooter
      :count="count"
      @changeFn="changeFnn"
      @clear="clearFn"
    ></TodoFooter>
  </div>
</template>

<script>
import TodoFooter from './components/TodoFooter.vue';
import TodoHeader from './components/TodoHeader.vue';
import TodoMain from './components/TodoMain.vue';
export default {
  data() {
    return {
      list: JSON.parse(localStorage.getItem('list')) || [],
      getSel: 'all',
    };
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    addFn(val) {
      const id = this.list[this.list.length - 1]
        ? this.list[this.list.length - 1].id + 1
        : 100;
      this.list.push({
        id,
        name: val,
        isDone: false,
      });
    },
    delFnn(val) {
      const index = this.list.findIndex((ele) => (ele.id = val));
      this.list.splice(index, 1);
    },
    changeFnn(val) {
      this.getSel = val;
    },
    clearFn() {
      this.list.forEach((ele) => (ele.isDone = false));
    },
  },
  computed: {
    count() {
      return this.list.filter((ele) => !ele.isDone).length;
    },
    showList() {
      if (this.getSel == 'no') {
        return this.list.filter((ele) => !ele.isDone);
      } else if (this.getSel == 'yes') {
        return this.list.filter((ele) => ele.isDone);
      } else {
        return this.list;
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler(val) {
        localStorage.setItem('list', JSON.stringify(val || []));
      },
    },
  },
};
</script>

<style></style>
