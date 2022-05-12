<template>
  <div class="counter" v-if="loading">
    <section class="text-3xl flex justify-center flex-col mx-auto text-center">
      <h5 v-if="!expired">Timer Counter</h5>
      <h5 v-else>Timer is done</h5>
    </section>
    <section class="flex text-6xl justify-center content-center">
      <div class="days mr-2 relative">
        {{ dsiplayDays }}
        <div class="label text-sm absolute">days</div>
      </div>
      <span class="leading-sung">:</span>
      <div class="days mx-2 relative">
        {{ displayHours }}
        <div class="label text-sm absolute">hours</div>
      </div>
      <span class="leading-sung">:</span>
      <div class="days mx-2 relative">
        {{ displayMinutes }}
        <div class="label text-sm absolute">minutes</div>
      </div>
      <span class="leading-sung">:</span>
      <div class="days ml-2 relative">
        {{ displaySeconds }}
        <div class="label text-sm absolute">seconds</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "",
  props: ["year", "month", "date", "hour", "minute", "second", "millisecond"],
  data: () => ({
    dsiplayDays: 0,
    displayHours: 0,
    displayMinutes: 0,
    displaySeconds: 0,
    loading: false,
    expired: false,
  }),
  computed: {
    _seconds: () => 1000,
    _mintues() {
      return this._seconds * 60;
    },
    _hours() {
      return this._mintues * 60;
    },
    _days() {
      return this._hours * 24;
    },
    end() {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hour,
        this.minute,
        this.second,
        this.millisecond
      );
    },
  },
  mounted() {
    this.showReamining();
  },
  methods: {
    formatNum(num) {
      return num < 10 ? "0" + num : num;
    },
    showReamining() {
      const timer = setInterval(() => {
        const now = new Date();
        // const end = new Date(2023, 4, 13, 10, 10, 10, 10);
        const distance = this.end.getTime() - now.getTime();
        if (distance <= 0) {
          clearInterval(timer);
          this.expired = true;
          this.loading = true;
          return;
        }
        const days = Math.floor(distance / this._days);
        const hours = Math.floor((distance & this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._mintues);
        const seconds = Math.floor((distance % this._mintues) / this._seconds);
        this.displayMinutes = this.formatNum(minutes);
        this.displaySeconds = this.formatNum(seconds);
        this.displayHours = this.formatNum(hours);
        this.dsiplayDays = this.formatNum(days);
        this.loading = true;
      }, 1000);
    },
  },
};
</script>

<style scoped>
.seconds {
  max-width: 60px;
}
</style>
