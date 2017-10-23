<template>
  <div class="demo">
    <virtual-scroller
      class="scroller"
      :items="items"
      keyField="key"
      content-tag="table"
      item-height="50"
      type-field="type"
      page-mode
      ref="scroller"
    >
      <template slot-scope="props">
        <tr v-if="props.item.type === 'letter'" class="letter item" :key="props.itemKey">
          <td>
            {{props.item.value}} Scoped
          </td>
        </tr>

        <tr v-if="props.item.type === 'person'" class="person item" :key="props.itemKey">
          <td v-for="i in 3"
            :key="i"
          >
            {{props.item.value.name}}
          </td>
        </tr>
      </template>
    </virtual-scroller>
  </div>
</template>

<script>
// import Letter from './components/Letter.vue'
// import Item from './components/Item.vue'
import faker from 'faker'

// Data with a type field
const items = [
  { key: '-1', type: 'letter', value: 'A' }
]

for (let i = 0; i < 1000; i++) {
  const doc = { key: i, type: 'person', value: { name: faker.address.city() } }
  items.push(doc)
}

// Bind the components to the item type
// const renderers = Object.freeze({
//   letter: Letter,
//   person: Item
// })

export default {
  data: () => ({
    items
    // renderers
  }),
  mounted () {
    setTimeout(function () {
      console.log('Scroll:', this.$refs.scroller)
      this.$refs.scroller.scrollToItem(500)
    }.bind(this, 1000))
  }
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
