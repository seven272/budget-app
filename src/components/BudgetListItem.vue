/* eslint-disable vue/return-in-computed-property */
<template>
<div>
    <div class="list-item" v-for='(item, prop) in list' :key='prop'>
     
     <span class="el-icon-top" v-if="item.value > 0"></span>
     <span class="el-icon-bottom" v-else></span>
     <span class="budget-comment"> {{item.comment}} </span>
     <span class="budget-value" :style="{color: item.type === 'INCOME' ? 'green' : 'red'}"> {{item.value}} </span>
    <ElButton type="danger" size="mini" @click="deleteItem(item.id)">DELETE</ElButton>
   </div>
  </div>
</template>
<script>

export default {
 name: "BudgetListItem",
 props: {
  list: {
   type: Object,
   default: () => ({}),
  }
 },
 data: ()=> ({
  
 }),
 computed: {
  
//    btn: function() {
//     return Object.values(this.list).forEach((element) => {
//          if (element.value > 0) {
//            console.log("plus");
//          } else {
//            console.log("minus");
//          }
         
//      })
//  }
 },
 methods: {
  deleteItem(id) {
   this.$emit("deleteItem", id)
  },
  // showtest() {
  //   console.log("ghjfkfff");
  // }
 }
}
</script>
<style scoped>
 .list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
 }

 .budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
 }
 
</style>