<template>
  <div class="app-container relative">
    <FilterTool :filterList="filterList" :formData="filterValue"></FilterTool>
    <div class="mt-[20px]">
      <el-button @click="add" icon="CirclePlus" type="primary">
        新增用户
      </el-button>
      <el-button icon="Download" type="info">导出用户</el-button>
      <el-button icon="Delete" type="danger">批量删除用户</el-button>
    </div>
    <div class="mt-[20px]">
      <el-table
        v-loading="loading"
        :data="tableList"
        @selection-change="handleSelectionChange"
      >
        <el-table-column type="selection" width="55"></el-table-column>
        <el-table-column
          v-for="(item, key) in columns"
          :key="key"
          :label="item.label"
          :prop="item.prop"
        >
        </el-table-column>
        <el-table-column label="状态">
          <template #default="scope">
            <el-switch
              style="
                --el-switch-on-color: #13ce66;
                --el-switch-off-color: #ff4949;
              "
              inline-prompt
              active-text="启用"
              inactive-text="禁用"
            />
          </template>
        </el-table-column>
        <el-table-column
          label="操作"
          align="center"
          width="200"
          class-name="small-padding fixed-width"
        >
          <template #default="scope">
            <el-button type="success" @click="handlePreview(scope.row)" link
              >查看</el-button
            >
            <el-button type="primary" @click="handleEdit(scope.row)" link
              >编辑</el-button
            >
            <el-button type="danger" @click="handleRemove(scope.row)" link
              >删除</el-button
            >
          </template>
        </el-table-column>
      </el-table>
    </div>
    <div class="relative">
      <pagination
        :total="total"
        v-model:page="pageNum"
        v-model:limit="pageSize"
        @pagination="getTableList"
      />
    </div>
    <add-new-personal
      @confirmUserData="addNewPersonalConfirm"
      v-model="addNewPersonalVisible"
      @close="closeAddNewPersonal"
    ></add-new-personal>
  </div>
</template>

<script setup>
import FilterTool from '@/components/FilterTool.vue'
import addNewPersonal from '@/components/Modal/addNewPersonal.vue'
import { ref, onMounted } from 'vue'

onMounted(() => {
  getTableList()
})
const addNewPersonalVisible = ref(false)
const tableList = ref([])
const pageNum = ref(1)
const pageSize = ref(10)
const total = ref(0)
const columns = [
  { label: '昵称', prop: 'nickName', width: '' },
  { label: '姓名', prop: 'trueName', width: '' },
  { label: '手机号', prop: 'phone', width: '' },
  { label: '来源渠道', prop: 'registChannel', width: '' },
  { label: '责任教练', prop: 'responsibilityName', width: '' },
  { label: '会籍顾问', prop: 'consultantName', width: '' },
  { label: '所属分销商', prop: '', width: '' },
  { label: '备注', prop: 'notes', width: '' },
  { label: '注册日期', prop: 'registTime', width: '' },
]
const loading = ref(false)
const filterList = ref([
  {
    type: 'input',
    props: 'name',
    placeholder: '请输入会员昵称',
    width: '150px',
  },
  {
    type: 'input',
    props: 'phone',
    placeholder: '请输入手机号',
    width: '150px',
  },
  {
    type: 'date',
    props: 'date',
    placeholder: '请选择日期',
    width: '150px',
  },
  {
    type: 'select',
    props: 'channel',
    placeholder: '请选择渠道',
    width: '150px',
    options: [
      { value: '小程序', label: '小程序' },
      { value: '美团', label: '美团' },
      { value: '地推', label: '地推' },
      { value: '其他', label: '其他' },
    ],
  },
  {
    type: 'button',
    label: '搜索',
    btnType: 'primary',
    click: handleFilter,
  },
  {
    type: 'button',
    label: '重置',
    btnType: 'default',
    click: hacnleReset,
  },
])
const filterValue = ref({
  name: '',
  phone: '',
  date: '',
})
function handleFilter(data) {
  console.log(data)
}
function hacnleReset() {
  filterValue.value = {
    name: '',
    phone: '',
    date: '',
  }
}
function handleSelectionChange() {}
function handlePreview(row) {
  console.log(row)
}
function handleEdit(row) {
  console.log(row)
}
function handleRemove(row) {
  console.log(row)
}
function getTableList() {
  console.log(pageSize.value, pageNum.value)
}
function closeAddNewPersonal() {}
function add() {
  addNewPersonalVisible.value = true
}
function addNewPersonalConfirm(data) {
  console.log('data', data)
  addNewPersonalVisible.value = false
}
</script>
