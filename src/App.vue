<template>
  <div id="app">
    <div class="container">
      <div class="form-group mt-5">
        <label for="txtBox">
          <h5>Vuertual Numeric Keyboard</h5>
        </label>
        <input
          type="text"
          class="form-control"
          v-model="value"
          id="txtBox"
          placeholder="Press any button"
        />
      </div>
      <Keyboard @pressed="value = $event" :selfValue="value"></Keyboard>
    </div>
  </div>
</template>

<script>
import Keyboard from './components/Keyboard.vue';

export default {
  components: { Keyboard },
  data() {
    return {
      value: '',
    };
  },
};
</script>

<style scoped>
.container {
  max-width: 300px;
}
</style>
