<template>
  <div class="todo">
    <h1>Todo List</h1>
    <InputText v-model="inputItem" class="text-black" @keyup.prevent.enter="addItem" size="small" />
    <div class="mt-10">
      <ul class="list-disc">
        <li v-for="(item, idx) in todoItems" :key="idx" class="cursor-pointer flex flex-row">
          <div class="align-middle">
            <Checkbox v-model="item.status" :binary="true" class="mr-3" />
          </div>

          <div :class="{ 'line-through': item.status }" @click="toggleComplete(item)">
            {{ item.text }}
          </div>

          <div class="ml-6 text-red-500 hover:text-xl" @click="removeItem(item)">X</div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import InputText from 'primevue/inputtext'
import Checkbox from 'primevue/checkbox'
import { computed, ref } from 'vue'

interface ItemIfc {
  id: string
  text: string
  status: 1 | 0
}

const inputItem = ref(''),
  todoItems = ref<
    Array<{
      id: string
      text: string
      status: 1 | 0
    }>
  >([])

function addItem() {
  todoItems.value.push({
    id: inputItem.value,
    text: inputItem.value,
    status: 0
  })

  inputItem.value = ''
}

function toggleComplete(item: ItemIfc) {
  const found = todoItems.value.find((it) => it == item)

  if (found) {
    found.status = item.status === 1 ? 0 : 1
  }
}

function removeItem(item: ItemIfc) {
  todoItems.value.splice(
    todoItems.value.findIndex((it) => it == item),
    1
  )
}
</script>

<style></style>
