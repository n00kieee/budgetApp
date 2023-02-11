<template>
  <el-card class="form-card">
    <el-form v-model="formData" :rules="rules" ref="addItemForm" label-position="top">
      <el-form-item label="Type" prop="type">
        <el-select class="type-select" v-model="formData.type" placeholder="Choose type">
          <el-option lable="Income" value="INCOME"/>
          <el-option lable="Outcome" value="OUTCOME"/>
        </el-select>
      </el-form-item>
      <el-form-item label="Comment" prop="comment">
        <el-input v-model="formData.comment"/>
      </el-form-item>
      <el-form-item label="Value" prop="value">
        <el-input v-model.number="formData.value"/>
      </el-form-item>
      <el-button @click="onSubmit" type="primary">Submit</el-button>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name: "Form",
  data: () => ({
    formData: {
      type: '',
      comment: '',
      value: ''
    },
    rules: {
      type: [
        {
          required: true,
          message: 'Please select type',
          trigger: 'change'
        }
      ],
      comment: [
        {
          required: true,
          message: 'Please input comment',
          trigger: 'blur'
        }
      ],
      value: [
        {
          required: true,
          message: 'Please input comment',
          trigger: 'change'
        },
        {
          type: 'number',
          message: 'Value must be a number',
          trigger: 'change'
        }
      ],
    },
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          this.$emit('submitForm', { ...this.formData });
          this.$refs.addItemForm.resetFields();
        }
      })
    },
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