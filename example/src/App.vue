<template>
  <div class="demo">
    <virtual-scroller
      class="scroller"
      :items="items"
      :renderers="renderers"
      item-height="50"
      type-field="type">
    </virtual-scroller>
  </div>
</template>

<script>
import Letter from './components/Letter.vue'
import Item from './components/Item.vue'
import faker from 'faker'

// Data with a type field
const items = [
  { type: 'letter', value: 'A' }
]

for (let i = 0; i < 1000; i++) {
  const doc = { type: 'person', value: { name: faker.address.city() } }
  items.push(doc)
}

// Bind the components to the item type
const renderers = Object.freeze({
  letter: Letter,
  person: Item
})

export default {
  data: () => ({
    items,
    renderers
  })
}
</script>

<style>
.scroller {
  height: 100%;
}

.scroller .item {
  height: 50px;
}
</style>
