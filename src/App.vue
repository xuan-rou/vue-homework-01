<script setup>
import { ref } from 'vue'

const drinks = ref([
  { id: 1, name: '珍珠奶茶', describe: '香濃奶茶搭配QQ珍珠', price: 50, stock: 20 },
  { id: 2, name: '冬瓜檸檬', describe: '清新冬瓜配上新鮮檸檬', price: 45, stock: 18 },
  { id: 3, name: '翡翠檸檬', describe: '綠茶與檸檬的完美結合', price: 55, stock: 34 },
  { id: 4, name: '四季春茶', describe: '香醇四季春茶，回甘無比', price: 45, stock: 10 },
  { id: 5, name: '阿薩姆奶茶', describe: '阿薩姆紅茶搭配香醇鮮奶', price: 50, stock: 25 },
  { id: 6, name: '檸檬冰茶', describe: '檸檬與冰茶的清新組合', price: 45, stock: 20 },
  { id: 7, name: '芒果綠茶', describe: '芒果與綠茶的獨特風味', price: 55, stock: 18 },
  { id: 8, name: '抹茶拿鐵', describe: '抹茶與鮮奶的絕配', price: 60, stock: 20 }
])

const tempEdit = ref({
  id: '',
  name: '',
  describe: '',
  price: '',
  stock: ''
})

const addStock = (drink) => {
  drink.stock++
}
const reduceStock = (drink) => {
  if (drink.stock <= 0) drink.stock == 0
  else drink.stock--
}
const editItemName = (drink) => {
  tempEdit.value = { ...drink }
}
const confirmEdit = () => {
  const index = drinks.value.findIndex((item) => item.id === tempEdit.value.id) //抓取陣列index
  drinks.value[index] = tempEdit.value
  tempEdit.value = ''
}
const editCancel = () => {
  tempEdit.value = ''
}
</script>

<template>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
        <th scope="col">編輯名稱</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="drink in drinks" :key="drink.id">
        <td>
          <p class="cursor-pointer">{{ drink.name }}</p>
        </td>
        <td>
          <small>{{ drink.describe }}</small>
        </td>
        <td class="item_price">{{ drink.price }}</td>
        <td>
          <button @click="reduceStock(drink)">-</button>
          <span class="item_stock">{{ drink.stock }}</span>
          <button @click="addStock(drink)">+</button>
        </td>
        <td><button type="button" @click="editItemName(drink)">編輯</button></td>
      </tr>
    </tbody>
  </table>
  <div>
    <h4>編輯區</h4>
    <p class="cursor-pointer">待編輯名稱：{{ tempEdit.name }}</p>
    <input type="text" v-model="tempEdit.name" />
    <button type="button" @click="confirmEdit(drink)">確認</button>
    <button type="button" @click="editCancel">取消</button>
  </div>
</template>

<style scoped>
.item_price {
  text-align: center;
}
.item_stock {
  min-width: 35px;
  text-align: center;
  padding: 0 4px;
  display: inline-block;
}
.cursor-pointer {
  cursor: pointer;
}
</style>
