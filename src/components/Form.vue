<template>
 <ElCard class="form-card">
  <ElForm :model="formData" ref="addItemForm" :rules="rules" label-position="top">
   <ElFormItem label="Type" prop="type">
    <ElSelect class="type-select" v-model="formData.type" placeholder="Выбираем тип...">
     <ElOption label="Income" value="INCOME" />
     <ElOption label="Outcome" value="OUTCOME"/>
    </ElSelect>
   </ElFormItem>
   <ElFormItem label="Comments" prop="comment">
    <ElInput v-model="formData.comment"/>
   </ElFormItem>
   <ElFormItem label="Value" prop="value">
    <ElInput v-model.number="formData.value"/>
   </ElFormItem>
   <ElButton @click="onSubmit" type="primary">Submit</ElButton>
  </ElForm>
 </ElCard>
</template>
<script>

export default {
 name: "Form",
 data: () => ({
  formData: {
   type: "INCOME",
   comment: "",
   value: 0,
  },
  rules: {
   type: [
    {required: true, message: "Выберите значение...", trigger: "blur"}
    ],
   comment: [
    {required: true, message: "Наберите текст...", trigger: "change"}
   ],
   value: [
    {required: true, message: "Введите значение", trigger: "change"},
    {type: "number", message: "Только цифры", trigger: "change"}
   ]
 },
 }),
  
 methods: {
  onSubmit() {
   // console.log(this.$refs.addItemForm)
   this.$refs.addItemForm.validate((valid) => {
    if(valid) {
     this.$emit("submitForm", { ...this.formData });
     this.$refs.addItemForm.resetFields()
    }
   })
  }
 },

}
</script>
<style scoped>
.form-card {
 max-width: 500px;
 margin: 0 auto;
}
 .type-select {
  width: 100%;
 }

 
</style>
