<template>
  <div class="my-table">
    <el-table :data="tableData" style="width: 100%" border>
      <el-table-column prop="id" label="序号" width="150px" align="center"></el-table-column>
      <el-table-column prop="name" label="用户名" align="center">
        <template #default="scope">
          <template v-if="scope.row.isEdit">
            <el-input
              v-model="scope.row.name"
              clearable
              style="width: 60%; margin-right: 20px"
              ref="inputRef"
            ></el-input>
            <el-button type="success" size="small" @click="handleSave(scope.row)">保存</el-button>
            <el-button size="small" @click="handleCancel(scope.row)">取消</el-button>
          </template>
          <span v-else>{{ scope.row.name }}</span>
        </template>
      </el-table-column>
      <el-table-column prop="cellphone" label="电话号码" align="center"> </el-table-column>
      <el-table-column label="操作" width="100" align="center">
        <template #default="scope">
          <el-button @click.prevent="handleEdit(scope.row)" type="text" size="small">编辑</el-button>
          <el-button type="text" size="small" @click.prevent="handleDelete(scope.$index, tableData)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  props: {
    tableData: {
      type: Array,
      required: true
    }
  },
  setup() {
    const inputRef = ref(null)
    let oldValue
    const handleEdit = row => {
      oldValue = row.name
      row.isEdit = true
    }
    const handleSave = row => {
      row.isEdit = false
    }
    const handleCancel = row => {
      row.name = oldValue
      row.isEdit = false
    }
    const handleDelete = (index, rows) => {
      rows.splice(index, 1)
    }
    return {
      inputRef,
      handleEdit,
      handleSave,
      handleDelete,
      handleCancel
    }
  }
}
</script>

<style scoped></style>
