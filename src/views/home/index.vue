<template>
  <div class="home container">
    <el-card shadow="hover">
      <avue-crud class="table-content" ref="fatherTableRef" :option="fatherOption" :data="data" @search-change="search" @row-save="save">
        <template #menu="{ size, row, index }">
          <el-button v-if="!row.isEnd" @click="addType(row, index)" icon="el-icon-circle-plus" text type="primary"
            :size="size"></el-button>
          <el-button v-else @click="editType(row, index)" icon="el-icon-edit" text type="primary"
            :size="size"></el-button>
        </template>
      </avue-crud>
    </el-card>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue'
//  定义父级表格ref
const fatherTableRef = ref<any>(null)
// 搜索值
const searchObj = reactive({
  text: '',
})
// 表格数据
const data = reactive([
  {
    id: 1,
    text: '文本1',
    isEnd: false,
    children: [
      {
        id: 11,
        text: '文本1-1',
        isEnd: true,
      },
      {
        id: 12,
        text: '文本12',
        isEnd: true,
      },
    ],
  },
  {
    id: 2,
    text: '文本2',
    isEnd: false,
    children: [
      {
        id: 21,
        text: '文本2-1',
        isEnd: true,
      },
    ],
  },
])
// 父表格配置项
const fatherOption = reactive({
  searchIndex: 3,
  border:true,
  expandRowKeys: ['1'],
  emptyBtn: false,
  addTitle: '新增111',
  header: false,
  showHeader: false,
  searchIcon: true,
  searchMenuSpan: 2,
  editBtn: false,
  delBtn: false,
  addBtn: false,
  column: [
    {
      label: '内容',
      prop: 'text',
      search: true,
    },
  ],
})
// 子表格配置项
const sonOption = reactive({
  header: true,
  showHeader: false,
  editBtn: true,
  // delBtn: false,
  // addBtn: false,
  column: [
    {
      label: '内容',
      prop: 'text',
    },
  ],
})
// 表格新增类型
const addType = (row: any, index: number) => {
  console.log('新增子类', row, index, fatherTableRef.value)
  fatherTableRef.value.rowAdd()
}
// 表格编辑类型
const editType = (row: any, index: number) => {
  console.log('编辑子类', row, index)
  fatherTableRef.value.rowEdit(row,index)
}
// 搜索方法
const search = (data: any) => {
  console.log('搜索', data, searchObj)
}
// 保存
const save = (row: any,done: any,loading: any) => {
console.log('保存',row,done,loading);
done()

}
</script>
<style scoped lang="scss">
.home {
  height: 100%;
}

::v-deep .el-form-item__label {
  display: none;
}
// ::v-deep .table-content .el-table__body{
//   border:1px  solid red;
// }
</style>
