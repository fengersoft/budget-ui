<template>
    <div>
        <div class="item">
            <div class="itemSxh">{{ item.sxh }}</div>
            <el-form-item label="预算名称" class="itemName">
                <el-input v-model="item.name" placeholder="请输入预算名称"></el-input>
            </el-form-item>
            <el-form-item label="预算金额" class="itemValue">
                <el-input v-model="item.price" placeholder="请输入预算金额"></el-input>
            </el-form-item>
            <el-button type="danger" link  class="btnDelete" @click="onDeletItem(item.id)">删除</el-button>
           

        </div>
    </div>
  </template>
  

  <script setup>
    
    
    const {item}=defineProps({
        item:Object,

    })

    const emit=defineEmits(['deleteItem'])
    

  const onDeletItem=(id)=>{


    emit('deleteItem',id)
  }
    
    
    
   

    
</script>
<style scoped>
.item{
    display: flex;
    align-items: center;
   
    width: 100%;
   
}
.itemName{
    margin-right: 20px;
}
.itemName,itemValue{
    justify-items: center;
}
.itemSxh{
    width: 48px;
    height: 100%;
    text-align: center;
    margin-bottom: 16px;
    font-weight: bold;
}
.btnDelete{
    margin-bottom: 16px;
    margin-left: 16px;
   
}


</style>     