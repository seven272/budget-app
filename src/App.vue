<template>
  <div id="app">
    <Form @submitForm="onFormSubmit" />
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" />
    <!-- <BudgetList :list="list" @deleteItem="onDeleteItem" /> -->
  </div>
</template>

<script>
import BudgetList from './components/BudgetList.vue'
import TotalBalance from './components/TotalBalance.vue'
import Form from './components/Form.vue'

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
        comment: 'Какой-то комментарий',
        id: 1,
        // bntIsVisible: true,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Какой-то исходящий комментарий',
        id: 2,
        // bntIsVisible: false,
      },
    }
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => {
          if(item.type === 'INCOME') {
            return acc + item.value
          } else if(item.type === 'OUTCOME') {
            return acc - item.value
          }
        }, 0
      )
    },
  },
  methods: {
    // onDeleteItem(id) {
    //   this.$delete(this.list, id)
    // },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      }
      this.$set(this.list, newObj.id, newObj)
    },
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
