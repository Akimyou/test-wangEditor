<template>
  <div>
    <el-row>
      <el-col :span="22"
        ><el-input :value="modelValue" placeholder="请输入内容" disabled
      /></el-col>
      <el-col :span="2" style="padding-left: 8px; padding-right: 8px"
        ><el-button
          type="primary"
          :icon="Edit"
          circle
          @click="handleOpenEditor"
      /></el-col>
    </el-row>
    <el-dialog
      v-model="dialogVisible"
      title="Editor"
    >
      <Editor ref="editorCpRef"></Editor>
      <template #footer>
        <span class="dialog-footer">
          <el-button @click="dialogVisible = false">Cancel</el-button>
          <el-button type="primary" @click="handleConfirm">
            Confirm
          </el-button>
        </span>
      </template>
    </el-dialog>
  </div>
</template>

<script lang="ts" setup>
import { Edit } from "@element-plus/icons-vue";
import Editor from "./Editor.vue";
import { nextTick, ref } from "vue";

const props = defineProps({
  modelValue: String
})

const emit = defineEmits(["update:modelValue"]);

const editorCpRef = ref();

const dialogVisible = ref(false);

const handleConfirm = () => {
  emit('update:modelValue', editorCpRef.value.editorRef.getHtml())
  dialogVisible.value = false
};

const handleOpenEditor = async () => {
  dialogVisible.value = true
  await nextTick()
  editorCpRef.value.valueHtml = props.modelValue
}
</script>

<style scoped>
.dialog-footer button:first-child {
  margin-right: 10px;
}
</style>