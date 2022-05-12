<template>
  <div class="home">
    <Counter
      :year="2023"
      :month="4"
      :date="12"
      :hour="23"
      :minute="60"
      :second="59"
      :millisecond="31"
    />
  </div>
</template>

<script>
import Counter from "../components/Counter.vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "",
  components: {
    Counter,
  },
};
</script>
