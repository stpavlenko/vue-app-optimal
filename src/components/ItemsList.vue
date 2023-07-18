<script setup>
import { onMounted, ref } from 'vue'

const itemsLength = 25
const items = ref([])
const selectedItemId = ref(null)

function fillItems() {
  for (let i = 1; i <= itemsLength; i++) {
    items.value.push({
      id: i,
      name: `foo${i}`,
      value: `bar${i}`
    })
  }
}

function selectItem(id) {
  selectedItemId.value = id
}

onMounted(() => {
  fillItems()
})
</script>
<template>
  <label v-if="selectedItemId">
    <span>Value:</span>
    <input
      type="text"
      class="form-control"
      v-model="items.find((item) => item.id === selectedItemId).value"
    />
  </label>
  <ul class="list-group">
    <li
      tabindex="0"
      @click="selectItem(item.id)"
      @keyup.enter="selectItem(item.id)"
      v-for="item in items"
      :key="item.id"
      class="list-group-item list-group-item-action"
      :class="{ active: selectedItemId === item.id }"
    >
      <span>Name: {{ item.name }}</span>
      <span>Value: {{ item.value }}</span>
    </li>
  </ul>
</template>
<style lang="scss" scoped>
span {
  display: block;
}
ul {
  margin-top: 0.5rem;
}
.list-group-item {
  cursor: pointer;
}
</style>
