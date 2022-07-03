<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ listSum }}</strong></span
    >
    <ul class="filters">
      <li>
        <a
          :class="{ selected: isOk == 'all' }"
          href="javascript:;"
          @click="change('all')"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isOk == 'no' }"
          href="javascript:;"
          @click="change('no')"
          >未完成</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isOk == 'ok' }"
          href="javascript:;"
          @click="change('ok')"
          >已完成</a
        >
      </li>
    </ul>
    <button class="clear-completed">清除已完成</button>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      isOk: "all",
    };
  },
  props: ["listSum"],
  methods: {
    change(val) {
      this.isOk = val;
      this.$emit("upData", val);
    },
  },
};
</script>