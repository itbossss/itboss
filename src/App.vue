<template>
  <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader @add="addFn" @isChecked="isCheckedFn"></TodoHeader>
    <TodoMain :list="isShowList" @del="delFn"></TodoMain>
    <TodoFooter :count="count" @isSel="isSelFn" @clear="clearFn"></TodoFooter>
  </section>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
  data() {
    return {
      list: JSON.parse(localStorage.getItem('list')) || [],
      // list: [
      //   { id: 100, name: '吃饭', isDone: true },
      //   { id: 101, name: '睡觉', isDone: false },
      //   { id: 102, name: '打豆豆', isDone: true },
      // ],
      isSel: 'all',
    }
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    addFn(val) {
      this.list.push({
        id: this.list.length ? this.list[this.list.length - 1].id + 1 : 100,
        name: val,
        isDone: false,
      })
    },
    delFn(id) {
      const index = this.list.findIndex((item) => item.id == id)
      this.list.splice(index, 1)
    },
    isSelFn(val) {
      this.isSel = val
    },
    clearFn() {
      this.list = this.list.filter((item) => !item.isDone)
    },
    isCheckedFn(val) {
      this.list.forEach((item) => (item.isDone = val))
    },
  },
  computed: {
    count() {
      return this.list.filter((item) => !item.isDone).length
    },
    isShowList() {
      if (this.isSel === 'yes') {
        return this.list.filter((item) => item.isDone)
      } else if (this.isSel === 'no') {
        return this.list.filter((item) => !item.isDone)
      } else {
        return this.list
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler(val) {
        localStorage.setItem('list', JSON.stringify(val || []))
      },
    },
  },
}
</script>

<style></style>
