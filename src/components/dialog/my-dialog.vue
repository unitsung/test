<template>
  <el-dialog title="新增用户" v-model="dialogVisible" width="30%" center>
    <el-form :model="form" label-width="80px">
      <el-form-item label="编号">
        <el-input v-model="form.id"></el-input>
      </el-form-item>
      <el-form-item label="用户名">
        <el-input v-model="form.name"></el-input>
      </el-form-item>
      <el-form-item label="电话号码">
        <el-input v-model="form.cellphone"></el-input>
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="handleCancel">取 消</el-button>
        <el-button type="primary" @click="handleConfirm">确 定</el-button>
      </span>
    </template>
  </el-dialog>
</template>

<script>
import { ref } from 'vue'
export default {
  emits: ['addData'],
  setup(props, { emit }) {
    const dialogVisible = ref(false)
    const form = ref({
      id: '',
      name: '',
      cellphone: ''
    })
    const handleConfirm = () => {
      emit('addData', form.value)
      dialogVisible.value = false
    }
    const handleCancel = () => {
      dialogVisible.value = false
    }
    return {
      form,
      dialogVisible,
      handleConfirm,
      handleCancel
    }
  }
}
</script>

<style scoped></style>
