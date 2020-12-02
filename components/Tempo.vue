<template>
  <div>
    <div>{{ dynamicDateString }} dinamico</div>
    <div>{{ staticDateString }} estatico</div>
    <button @click="$fetch">Refresh</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mountains: [],
      staticDateString: null
    };
  },
  activated() {
    const date = new Date();
    console.log("oi");
    // Call fetch again if last fetch more than 30 sec ago
    console.log(new Date(this.$fetchState.timestamp));
    console.log(date);

    console.log(this.$fetchState.timestamp <= date);
    console.log(this.$fetchState.timestamp <= date - 30000);
    if (this.$fetchState.timestamp <= date - 30000) {
      console.log("refetch");
      this.$fetch();
    }
  },
  async fetch() {
    const delay = ms => new Promise(res => setTimeout(res, ms));
    const staticDate = new Date();
    const staticDateString = staticDate.toGMTString();
    console.log("Passando pelo fetch");
    await delay(5000);
    console.log("Passou");
    this.staticDateString = staticDateString;
  },

  computed: {
    dynamicDateString() {
      return new Date().toGMTString();
    }
  },
  methods: {}
};
</script>
