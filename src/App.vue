<template>
  <div id="app">
    <Form @submitForm="onFormSubmit" />
    <Totalbalance :total="Totalbalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import Totalbalance from '@/components/TotalBalance';
import Form from '@/components/Form';

export default {
  name: 'App',
  components: {
    BudgetList,
    Totalbalance,
    Form,
  },

  data: () => ({
    list: {
      1: {
        type: 'Income',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'Outcome',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
      }
    }

  }),

  computed: {
    Totalbalance() {
      return Object.values(this.list).reduce(
        (acc, item) => acc + item.value, 0)
    }
  },

  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
        const newObj = {
          ...data,
          id: String(Math.random()),
        };
      this.$set(this.list, newObj.id, newObj)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
