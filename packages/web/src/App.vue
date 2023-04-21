<template>
  <el-form :model="form" label-width="120px">
    <el-form-item label="InputDemo">
      <InputDemo v-model="form.inputDemoValue" />
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="onSubmit">Create</el-button>
      <el-button>Cancel</el-button>
    </el-form-item>
  </el-form>
</template>

<script lang="ts" setup>
import { reactive } from 'vue'
import InputDemo from './components/InputDemo.vue'

// do not use same name with ref
const form = reactive({
  inputDemoValue: ''
})

const onSubmit = () => {
  console.log('submit!', form)
}
</script>
