<template>
  <input v-model="textmsg" />
  <button @click="add">添加</button>
  <button @click="delCheck">清除已选数据</button>
  <!-- data -->
  <div v-if="lists.length">
    <div v-for="(item,index) in lists" :key="item.text">
      <input type="checkbox" v-model="item.todo" />
      <span :class="{done: item.todo}">{{item.text}}</span>
      <button @click="del(index)">删除</button>
    </div>
    <div>
      <span>{{hasCheck}}</span> / <span>{{lists.length}}</span>
    </div>
    <div>
      <span>全选</span>
      <input type="checkbox" v-model="allTodo" />
    </div>
  </div>

  <!-- no data -->
  <div v-else>
    暂无数据
  </div>
</template>

<script lang='ts' setup>
import {ref, computed} from 'vue'
const textmsg = ref<string>('');

interface Itodo {
  text: string
  todo: boolean
}
let lists = ref<Itodo[]>([
  {text: '吃饭', todo: true},
  {text: '睡觉', todo: false},
  {text: '学习', todo: false},
  {text: '打酱油', todo: true},
])
// 重点 computed参数可以是回调函数，也可以是一个对象
// has-checkbox
const hasCheck = computed(() => lists.value.filter((items) => items.todo).length)
// all checkbox
const allTodo = computed({
  get() {
    return hasCheck.value === lists.value.length // 手动设置hasCheck
  },
  set(val:boolean) {
    lists.value.forEach((item) => item.todo = val)
  }
})
// add 
const add = () => {
  if (textmsg.value) {
    lists.value.push({
      text: textmsg.value,
      todo: false
    })
  }
  textmsg.value = ''
}
// delete
const del = (index: number) => {
  lists.value.splice(index, 1) // 当前位置删除一条数据
}
//delCheck 删除已完成的数据
const delCheck = () => {
  // 我们只返回todo = false的数据，重构数据
  lists.value = lists.value.filter(item => !item.todo)
}
</script>
<style scoped>
.done {
  text-decoration: line-through;
  color: gray;
}
</style>