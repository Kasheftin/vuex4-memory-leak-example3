<template>
  <div>
    <p>
      There're {{ regularItemsCount }} regular items.
    </p>
    <p>
      Add <input v-model="addRegularItemsCount" type="number" style="width: 70px"> items in a regular way.
      <button @click="addRegularItems">
        Add
      </button>
      <button @click="clearRegularItems">
        Clear regular items
      </button>
    </p>
    <hr>
    <p>
      There're {{ frozenItemsCount }} frozen items.
    </p>
    <p>
      Add <input v-model="addFrozenItemsCount" type="number" style="width: 70px"> items, apply Object.freeze for each.
      <button @click="addFrozenItems">
        Add
      </button>
      <button @click="clearFrozenItems">
        Clear frozen items
      </button>
    </p>
  </div>
</template>

<script>
export default {
  data () {
    return {
      addRegularItemsCount: 100,
      addFrozenItemsCount: 100,
      regularItems: [],
      frozenItems: []
    }
  },
  computed: {
    regularItemsCount () {
      return this.regularItems.length
    },
    frozenItemsCount () {
      return this.frozenItems.length
    }
  },
  methods: {
    addRegularItems () {
      this.regularItems = [...this.regularItems, ...Array(Number(this.addRegularItemsCount)).fill().map(() => this.createHeavyItem(3))]
    },
    clearRegularItems () {
      this.regularItems = []
    },
    addFrozenItems () {
      this.frozenItems = [...this.frozenItems, ...Array(Number(this.addFrozenItemsCount)).fill().map(() => Object.freeze(this.createHeavyItem(3)))]
    },
    clearFrozenItems () {
      this.frozenItems = []
    },
    createHeavyItem (it, childrenCount = 10) {
      return {
        hashes: Array(10).fill('Lorem ipsum dolor sit amet.'),
        children: it ? Array(childrenCount).fill().map(() => this.createHeavyItem(it - 1, childrenCount)) : []
      }
    }
  }
}
</script>
