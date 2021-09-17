<template>
  <ElCard class="form-card">
    <ElForm :model="formData" ref="addItemForm" :rules="formRules" label-position="top">
      <ElFormItem label="Type" prop="type">
        <ElSelect class="type-select" v-model="formData.type" placeholder="Choose type...">
          <ElOption label="INCOME" value="Income" />
          <ElOption label="OUTCOME" value="Outcome" />
        </ElSelect>
      </ElFormItem>

      <ElFormItem label="Comments" prop="comment">
        <ElInput v-model="formData.comment"/>
      </ElFormItem>

      <ElFormItem label="Value" prop="value">
        <ElInput v-model.number="formData.value" />
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
    formRules: {
      type: [{ required: true, message: "Please select type", trigger: "blur" }],
      comment: [{ required: true, message: "Please leve a comment", trigger: "change" }],
      value: [
        { required: true, message: "Please write a value", trigger: "change" },
        { required: "number", message: "Value must be a number", trigger: "change"}
      ]
    }
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate((valid) => {
        if (valid) {
          this.$emit("submitForm", {...this.formData});
          this.$refs.addItemForm.resetFields();
        }
      });
    }
  }
}
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
}
.type-select {
  width: 100%;
}
</style>