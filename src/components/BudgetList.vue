<template>
 <div class="budget-list-wrap">
  <!-- передаем header данные из обьекта data тоже там назван header и связываем из v-bind -->
  <ElCard :header="header">
    <el-button type="info" class="sort_button sort_button-all" @click="onShowAllItems">Все</el-button>
    <el-button type="info" class="sort_button sort_button-minus" @click="onShowOutcomeItems">Расходы</el-button>
    <el-button type="info" class="sort_button sort_button-plus" @click="onShowIncomeItems">Доходы</el-button>
   <!-- <template v-if="!isEmpty"> -->
   <template v-if="allItemsVisible">
    <BudgetListItem :list="list" @deleteItem="onDeleteItem"/>
   </template> 
   <template v-else-if="outComeItemsVisible">
     <BudgetListItem :list="onShowOutcomeItems()" @deleteItem="onDeleteItem"/>
    <p>Расходы</p>
   </template> 
   <template v-else-if="inComeItemsVisible">
     <BudgetListItem :list="onShowIncomeItems()" @deleteItem="onDeleteItem"/>
    <p>Доходы</p>
   </template> 
   <!-- <el-alert v-else type="info" :title="titleEmpty" :closable="false"/> -->
   <template v-else-if="isEmpty">
    <p>Задач в списке нет</p>
   </template> 
  </ElCard>
 </div>
</template>
<script>
import BudgetListItem from './BudgetListItem.vue' 

export default {
 name: "BudgetList",
 props: {
  list: {
   type: Object,
   default: () => ({}),
  }
 },
 components: {
  BudgetListItem,

 },
 data: () => ({
  header: "Список операций",
  titleEmpty: "Нет никаких операций прихода и расхода. Список пуст!",
  dialogVisible: false,
  allItemsVisible: true,
  inComeItemsVisible: false,
  outComeItemsVisible: false,
 }),
 computed: {
  isEmpty() {
   return !Object.keys(this.list).length
  }
 },
 methods: {
  // deleteItem(id) {
  //  this.$emit("deleteItem", id)
  // },
  onDeleteItem(id) {
      let confirmItem = confirm("Удалить даннай пункт из списка?");
      if (confirmItem) {
        this.$delete(this.list, id)
      } else {
        alert("Пункт остается на месте")
      }
    },
  onClickPlusButton(evt) {
    this.$emit("listItemsPlus", evt);

  },
  onShowPlusItems() {
    let arrIncomeElements = [];
    Object.values(this.list).forEach((element) => {
         if (element.type === "INCOME") {
           console.log("plus");
           arrIncomeElements.push(element);
         } else {
           console.log("minus");
         }
         
     })

    const obj = Object.assign({}, arrIncomeElements);
    // console.log(arrIncomeElements);
    console.log(obj)

  },
  onShowAllItems() {
    this.allItemsVisible = true;
    this.outComeItemsVisible = false;
    this.inComeItemsVisible = false;
  },
  onShowIncomeItems() {
    this.allItemsVisible = false;
    this.outComeItemsVisible = false;
    this.inComeItemsVisible = true;
    let arrIncomeElements = [];
    //сначала получаем массив значений дальше проходимся по нему форичем, в нашем случаии отдельный элемент всего массива это обьект
    Object.values(this.list).forEach((element) => {
         if (element.type === "INCOME") {
          arrIncomeElements.push(element);
         } 
     })
    //преобразуем массив в обьект, чтобы не ругался эслинт, так как в пропс мы передаем обьект изначально
    const objIncomeElements = Object.assign({}, arrIncomeElements);
    return objIncomeElements;
  },
  onShowOutcomeItems() {
    this.allItemsVisible = false;
    this.outComeItemsVisible = true;
    this.inComeItemsVisible = false;
    let arrOutcomeElements = [];
    Object.values(this.list).forEach((element) => {
      if (element.type === "OUTCOME") {
          arrOutcomeElements.push(element);
        } 
     });
    const objOutcomeElements = Object.assign({}, arrOutcomeElements);
    return objOutcomeElements;
  },
 }
}
</script>
<style scoped>
 .budget-list-wrap {
  max-width: 500px;
  margin: 0 auto;
 }
 .sort_button {
  width: 30%;
 }

</style>