<template>
  <div class="wrapper">
    <FormComp :fileds="dates" v-model="dates" />
  </div>
  <div v-for="el in dates" :key="el.name">{{ el }}</div>
</template>

<script>
import jsonData from "./data.json";
import FormComp from "@/components/FormComp.vue";
export default {
  components: {
    FormComp,
  },
  data() {
    return {
      dates: [],
    };
  },

  mounted() {
    this.dates = jsonData;
  },
};
</script>

<style>
.wrapper {
  width: 600px;
  display: flex;
  justify-content: space-between;
  margin: 0 auto;
}
</style>
