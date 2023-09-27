<template>
	<div style="display: block; width: 100%;">
		
				<el-table :data="tableData" style="width: 100%">
				<el-table-column prop="name" label="商家名稱" width="150" />
				<el-table-column prop="sever" label="服務項目" width="120" />
				<el-table-column prop="date" label="日期" width="120" />
				<el-table-column prop="money" label="金額" width="120" />
				<el-table-column prop="address" label="地址" />
				<el-table-column prop="state" label="狀態" />
			</el-table>
			

	</div>
	
</template>

<script lang="ts" setup>
import { ref, reactive } from 'vue'
// const  tableData = ref([
//   {
//     date: '2016-05-01',
//     name: 'Tom',
//     state: 'California',
//     city: 'Los Angeles',
//     address: 'No. 189, Grove St, Los Angeles',
//     zip: 'CA 90036',
//   }
// ])
const tableData = [
  {
    name: 'XXXXX',
    sever: '美容',
    date: '2023/09/05',
    money: '1500',
    address: '台北市文山區XXXXXXXX',
    state: '已完成',
  },
  {
    name: 'XXXXX',
    sever: '攝影',
    date: '2023/09/05',
    money: '10000',
    address: '台北市文山區XXXXXXXX',
    state: '已取消',
  },
  {
    name: 'XXXXX',
    sever: '美容',
    date: '2023/09/30',
    money: '500',
    address: '台北市文山區XXXXXXXX',
    state: '已完成',
  },
  {
    name: 'XXXXX',
    sever: '美容',
    date: '2023/09/10',
    money: '8000',
    address: '台北市文山區XXXXXXXX',
    state: '已完成',
  }]


</script>

<style scoped>

</style>