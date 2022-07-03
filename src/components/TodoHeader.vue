<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
    <label for="toggle-all"></label>
    <!-- label 可以关联一个表单标签 -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keyup.enter="add"
      v-model.trim="textVal"
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
      textVal: "",
    };
  },
  methods: {
    add() {
      if (!this.textVal) return;
      this.$emit("add", this.textVal);
      this.textVal = "";
    },
  },
  computed: {
    isAll: {
      get() {
        return this.$parent.list.every((item) => item.isDone);
      },
      set(val) {
        this.$emit('isAll',val)
      },
    },
  },
};
</script>