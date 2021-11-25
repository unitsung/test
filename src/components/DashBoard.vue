<template>
  <div class="dashboard">
    <div class="header">
      <h2 class="title">用户列表</h2>
      <div class="control">
        <div class="left">
          <el-button type="primary" @click="handleNew" style="margin-bottom: 20px; margin-top: 10px"
            >新增用户</el-button
          >
        </div>
        <div class="search">
          <el-input
            placeholder="请输入内容"
            v-model="searchStr"
            clearable
            style="margin-right: 20px"
            @input="inputChange"
          ></el-input>
          <el-button type="primary" plain @click="search">立即搜索</el-button>
        </div>
      </div>
    </div>
    <div class="content">
      <my-table :table-data="tableData"></my-table>
      <my-dialog ref="dialogRef" @add-data="changeTableData"></my-dialog>
    </div>
  </div>
</template>

<script>
import MyTable from './table/my-table.vue'
import MyDialog from './dialog/my-dialog.vue'
import { ref } from 'vue'
export default {
  components: {
    MyTable,
    MyDialog
  },
  setup() {
    // userData
    const userData = [
      {
        id: 1,
        name: 'lyh',
        cellphone: 17754456666,
        isEdit: false
      },
      {
        id: 2,
        name: 'tom',
        cellphone: 18855556666,
        isEdit: false
      },
      {
        id: 3,
        name: 'kobe',
        cellphone: 16655556666,
        isEdit: false
      },
      {
        id: 4,
        name: 'lily',
        cellphone: 13355556666,
        isEdit: false
      },
      {
        id: 5,
        name: 'lucy',
        cellphone: 15566668888,
        isEdit: false
      }
    ]
    const tableData = ref(userData)
    const dialogRef = ref(null)
    const handleNew = () => {
      dialogRef.value.dialogVisible = true
    }
    const changeTableData = data => {
      tableData.value.push(data)
    }
    // search
    const searchStr = ref('')
    const search = () => {
      if (searchStr.value) {
        tableData.value = tableData.value.filter(data => {
          if (data.name.includes(searchStr.value)) {
            return true
          }
          if (data.id == searchStr.value) {
            return true
          }
          if (data.cellphone == searchStr.value) {
            return true
          }
        })
      } else {
        tableData.value = userData
      }
    }

    function debounce(fn, wait) {
      let timeout = null
      return function () {
        if (timeout) clearTimeout(timeout)
        timeout = setTimeout(() => {
          fn()
        }, wait)
      }
    }
    const inputChange = debounce(() => {
      tableData.value = userData
    }, 50)

    return {
      tableData,
      dialogRef,
      handleNew,
      changeTableData,
      searchStr,
      search,
      inputChange
    }
  }
}
</script>

<style scoped>
.dashboard {
  width: 80%;
  background-color: #f9f9f9;
  padding: 20px;
  box-sizing: border-box;
  margin: 100px auto;
}
.title {
  text-align: center;
}
.control {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.search {
  display: flex;
}
</style>
