<template>
 <div class="total-value" v-bind:style="{color:changeColor}">Balance: {{ total }}</div>
</template>
<script>

export default {
 name: "TotalBalance",
 props: {
  total: {
   type: Number,
   default: 0,
  }
 },
 computed: {
  changeColor() {
   let colorTotal =""
    if(this.total > 0) {
     colorTotal = "green"
   } else if (this.total < 0) {
     colorTotal = "red"
   } else {
     colorTotal = "black"
   }
   return colorTotal;
  }
 },
}
</script>
<style scoped>
 .total-value {
  padding: 20px;
  font-size: 26px;
  text-transform: uppercase;
  text-align: center;
 }
</style>
