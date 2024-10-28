<script setup>
import { computed, ref } from 'vue'
import {v4 as uuidv4} from 'uuid'
import BudgetItemView from './components/BudgetItemView.vue'
    const list=ref([])
    const budgetName=ref('')
    const budgetAllPrice=ref(0.0)

    const addItem=()=>{
      let obj={
        sxh:list.value.length+1,
        name:`项目 ${list.value.length+1}`,
        price:0.0,
        id:uuidv4()
      }
      list.value.push(obj)
      console.log(list.value)
    }
    const remainingPrice=computed(()=>{
      let sum=0.0
      for(let i=0;i<list.value.length;i++){
        sum+=Number(list.value[i].price)
      }
      return budgetAllPrice.value-sum
    })

    const onDeleteItem=(id)=>{
       console.log('删除')
       console.log(id)
       let index=list.value.findIndex(item=>item.id===id)
       console.log(index)
       list.value.splice(index,1)

       for(let i=0;i<list.value.length;i++){
        list.value[i].sxh=i+1
       }
    }
</script>

<template>

<div class="page">
    <el-container>
      <el-header class="header">
        <el-button type="primary" @click="addItem">添加分项</el-button>
      </el-header>
      <el-main class="client">
         <div>
          
           <el-form-item label="总预算名称">
             <el-input v-model="budgetName" placeholder="请输入总预算名称"></el-input>
           </el-form-item>
           <el-form-item label="总预算金额">
             <el-input v-model="budgetAllPrice" placeholder="请输入总预算金额"></el-input>
           </el-form-item>
         </div>
         <div class="items">
           <div v-for="(item,index) in list" :key="index">
             <BudgetItemView :item="item"  @deleteItem="onDeleteItem" />
           </div>
         </div>
         <div>
           
         </div>
      </el-main>
      <el-footer>共{{ list.length }}项目,剩余<span :class="{red:remainingPrice<0}">{{ remainingPrice }}元</span></el-footer>
    </el-container>
  </div>
</template>

<style scoped>
   .page{
     height: 100vh;
     width: 100vw;
     display: flex;
   }
   .header{
   height: 48px;
   width: 100%;
   display: flex;
   align-items: center;
   justify-content: flex-start;
 }
.red{
   color: red;
 }
 .items{
  width: 100%;
  flex: 1;
  overflow-y: scroll;
 }
 .client{
  display: flex;
  flex-direction: column;
 }
</style>
