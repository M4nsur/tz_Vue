<template>
  <div v-for="(items, group) in groupedItems" :key="group">
    <strong>{{ group }}</strong>
    <div class="form" v-for="(item, idx) in items" :key="idx">
      <div v-if="!item.accept">
        {{ item.name }}
        <p>
          <input type="text" v-model="item.value" />
        </p>
      </div>
      <div v-else>
        <form action="" @submit.prevent="acceptChange(item)">
          <input type="text" v-model="item.name" />
          <button class="accept">☑️</button>
          <input type="text" v-model="item.value" />
        </form>
      </div>
    </div>

    <button @click="addForm(group)" class="addBtn">+</button>
  </div>
</template>

<script>
export default {
  props: {
    fileds: {
      type: Array,
      required: true,
    },
  },

  computed: {
    groupedItems() {
      return this.fileds.reduce((groups, item) => {
        const key = item.group;
        if (!groups[key]) {
          groups[key] = [];
        }
        groups[key].push(item);
        return groups;
      }, {});
    },
  },
  methods: {
    addForm(group) {
      console.log(group);
      const newForm = {
        group: group,
        name: "",
        value: "",
        accept: true,
      };
      this.$emit("sendForm", newForm);
    },
    acceptChange(item) {
      if (item.name) {
        item.accept = false;
      }
    },
  },
};
</script>

<style>
.accept {
  background: none;
  text-align: center;
  border-style: none;
  width: 8px;
}

.form {
  padding: 5px;
  border: solid;
  width: 130px;
  box-sizing: border-box;
  margin-bottom: 5px;
}
input {
  width: 80px;
}

.addBtn {
  width: 130px;
  background-color: rgb(28, 114, 95);
  height: 15px;
  font-size: 8px;
  color: white;
  margin-bottom: 15px;
  border: none;
  cursor: pointer;
}
</style>
