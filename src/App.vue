<template>
  <div class="todoapp">
    <TodoHeader @add="addFn" />
    <TodoMain :list="showlist" @delList="delListFn" />
    <TodoFooter :count="count" @fliterdata="fliterdataFn" />
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data() {
    return {
      getSel: 'all',
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
    delListFn(theId) {
      const index = this.list.findIndex((ele) => ele.id == theId)
      this.list.splice(index, 1)
    },
    fliterdataFn(val) {
      this.getSel = val
    },
  },
  computed: {
    count() {
      return this.list.filter((ele) => !ele.isDone).length
    },
    showlist() {
      if (this.getSel == 'no') return this.list.filter((ele) => !ele.isDone)
      else if (this.getSel == 'yes')
        return this.list.filter((ele) => ele.isDone)
      else return this.list
    },
  },
}
</script>

<style></style>
