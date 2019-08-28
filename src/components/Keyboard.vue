<template>
  <div class="vuertual-numeric-keyboard bg-light rounded border p-3">
    <button
      v-for="key in keys"
      :key="key"
      @click="press(key)"
      class="btn btn-lg shadow-none"
      :class="keyTheme"
    >{{ key }}</button>
    <button class="btn btn-lg shadow-none" :class="buttonTheme" @click="clear()">&larr;</button>
    <button class="btn btn-lg shadow-none" :class="buttonTheme" @click="clear('all')">C</button>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.min.css';
import _ from 'lodash';

export default {
  props: ['selfValue'],
  data() {
    return {
      value: '',
      keys: [...Array(10).keys()],
      keyTheme: 'btn-keyboard',
      buttonTheme: 'btn-danger',
    };
  },
  methods: {
    shuffle() {
      this.keys = _.shuffle(this.keys);
    },
    press(key) {
      this.value = `${this.value}${key}`;
      this.shuffle();
    },
    clear(type) {
      if (type === 'all') this.value = '';
      else this.value = this.value.substring(0, this.value.length - 1);
    },
  },
  watch: {
    value() {
      this.$emit('pressed', this.value);
    },
    selfValue() {
      this.value = this.selfValue;
    },
  },
  created() {
    this.shuffle();
  },
};
</script>

<style scoped>
.vuertual-numeric-keyboard {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-gap: 10px;
}
.vuertual-numeric-keyboard .btn {
  font-weight: bold;
}
.btn-keyboard {
  background-color: #80b6ff;
  color: #ffffff;
}
</style>
