<template>
  <div class="todoapp">
    <TodoHeader @add="addFn" @setchecked="setcheckedFn" />
    <TodoMain :list="showlist" @delList="delListFn" />
    <TodoFooter
      :count="count"
      @fliterdata="fliterdataFn"
      @clearAll="clearAllFn"
    />
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
      list: JSON.parse(localStorage.getItem('list') || []),
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
    clearAllFn() {
      this.list.forEach((ele) => (ele.isDone = false))
    },
    setcheckedFn(val) {
      this.list.forEach((ele) => (ele.isDone = val))
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
  watch: {
    list: {
      handler(val) {
        localStorage.setItem('list', JSON.stringify(val || []))
      },
      deep: true,
    },
  },
}
</script>

<style></style>
