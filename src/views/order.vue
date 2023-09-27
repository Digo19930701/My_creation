<template>
	<div style="display: block; width: 100%;">
	<el-table
	  ref="multipleTableRef"
	  :data="tableData"
	  style="width: 100%"
	  @selection-change="handleSelectionChange"
	>
	  <el-table-column type="selection" width="55" />
	  <el-table-column label="日期" width="120">
		<template #default="scope">{{ scope.row.date }}</template>
	  </el-table-column>
	  <el-table-column property="name" label="商家名稱" width="120" />
	  <el-table-column property="sever" label="服務項目" width="120" />
	  <el-table-column property="money" label="金額" width="120" />
	  <el-table-column property="address" label="地址" show-overflow-tooltip />
	  <el-table-column property="state" label="狀態" show-overflow-tooltip />
	</el-table>
	<div style="margin-top: 10px">
	  <el-button style="background-color: #f8d479" @click="toggleSelection([tableData[1], tableData[2]])"
		>變更日期</el-button
	  >
	  <el-button style="background-color: #f8d479" @click="toggleSelection()">取消訂單</el-button>
	  
	</div>
</div>
  </template>
  
  <script lang="ts" setup>
  import { ref } from 'vue'
  import { ElTable } from 'element-plus'
  
  interface User {
	date: string
	name: string
	sever: string
	address: string
	money:string
	state:string
  }
  
  const multipleTableRef = ref<InstanceType<typeof ElTable>>()
  const multipleSelection = ref<User[]>([])
  const toggleSelection = (rows?: User[]) => {
	if (rows) {
	  rows.forEach((row) => {
		// TODO: improvement typing when refactor table
		// eslint-disable-next-line @typescript-eslint/ban-ts-comment
		// @ts-expect-error
		multipleTableRef.value!.toggleRowSelection(row, undefined)
	  })
	} else {
	  multipleTableRef.value!.clearSelection()
	}
  }
  const handleSelectionChange = (val: User[]) => {
	multipleSelection.value = val
  }
  
  const tableData: User[] = [
	{
	  date: '2023-08-10',
	  name: '歡樂美容',
	  sever:'美容',
	  money:'50000',
	  address: '台北市文山區XXXXXX',
	  state:'處理中'
	},
	{
	  date: '2023-08-30',
	  name: '歡樂美容',
	  sever:'美容',
	  money:'500',
	  address: '台北市文山區XXXXXX',
	  state:'服務完成'
	},
	{
	  date: '2025-08-20',
	  name: '歡樂美容',
	  sever:'美容',
	  money:'50000',
	  address: '台北市文山區XXXXXX',
	  state:'處理中'
	},
	
	
  ]
  </script>