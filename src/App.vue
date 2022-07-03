<template>
  <div class="todoapp">
    <TodoHeader @add="addFn" />
    <TodoMain :list="list" />
    <TodoFooter />
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data() {
    return {
      list: [
        { id: 100, name: '吃饭', isDone: true },
        { id: 101, name: '睡觉', isDone: false },
        { id: 103, name: '打豆豆', isDone: true },
      ],
    }
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    addFn(val) {
      const id = this.list.length ? this.list[this.list.length - 1].id + 1 : 1
      this.list.push({ id, name: val, isDone: false })
    },
  },
}
</script>

<style></style>
