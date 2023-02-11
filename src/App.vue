<template>
  <div class="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList.vue";
import TotalBalance from "@/components/TotalBalance.vue";
import Form from "@/components/Form.vue";

export default {
  name: 'app',
  components: {
    BudgetList,
    TotalBalance,
    Form,
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'INCOME',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
      }
    },
  }),
  methods: {
    onDeleteItem(id) {
      delete this.list[id]
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj)
    },
  },
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) =>
              acc + item.value,
          0
      )
    },
  },
}
</script>

<style scoped>

</style>
