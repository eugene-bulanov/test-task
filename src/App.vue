<template>
  <div class="grid-view">
    <div class="selected-left">
      <div
        v-for="(item, itemIndex) in selectedLeft"
        :key="itemIndex"
        class="item"
      >
        {{ item.name }}
      </div>
    </div>
    <div>
      <div v-if="selectedRight != null" class="item">
        {{ selectedRightItem.name }}
      </div>
    </div>
    <div class="items">
      <div
        v-for="(item, itemIndex) in itemsLeft"
        :key="itemIndex"
        :class="{ item: true, active: inLeftCollection(item.id) }"
        @click="selectLeft(item.id)"
      >
        {{ item.name }}
      </div>
    </div>
    <div class="items">
      <div
        v-for="(item, itemIndex) in itemsRight"
        :key="itemIndex"
        class="item"
        @click="selectRight(item.id)"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      itemsLeft: [
        {
          id: 1,
          name: "Shoes 1",
        },
        {
          id: 2,
          name: "Shoes 2",
        },
        {
          id: 3,
          name: "Shoes 3",
        },
        {
          id: 4,
          name: "Shoes 4",
        },
        {
          id: 5,
          name: "T-shirt 1",
        },
        {
          id: 6,
          name: "T-shirt 2",
        },
        {
          id: 7,
          name: "T-shirt 3",
        },
        {
          id: 8,
          name: "T-shirt 4",
        },
      ],
      itemsRight: [
        {
          id: 11,
          name: "Jacket 1",
        },
        {
          id: 12,
          name: "Jacket 2",
        },
        {
          id: 13,
          name: "Jacket 3",
        },
        {
          id: 14,
          name: "Jacket 4",
        },
        {
          id: 15,
          name: "Hoodie 1",
        },
        {
          id: 16,
          name: "Hoodie 2",
        },
        {
          id: 17,
          name: "Hoodie 3",
        },
        {
          id: 18,
          name: "Hoodie 4",
        },
      ],
      selectedLeft: [],
      selectedRight: null,
    }
  },
  computed: {
    selectedRightItem() {
      return this.itemsRight.find((item) => {
        return item.id == this.selectedRight
      })
    },
  },
  methods: {
    selectLeft(id) {
      if (
        this.selectedLeft.length >= 6 ||
        this.selectedLeft.filter((item) => {
          return item.id == id
        }).length > 0
      )
        return false

      this.selectedLeft.push(
        this.itemsLeft.find((item) => {
          return item.id == id
        })
      )
    },
    selectRight(id) {
      this.selectedRight = id
    },
    inLeftCollection(id) {
      return (
        this.selectedLeft.filter((item) => {
          return item.id == id
        }).length > 0
      )
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.grid-view {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}
.items {
  border: 2px #000 solid;
  display: grid;
  gap: 10px;
  grid-template-columns: repeat(3, 1fr);
  padding: 20px;
}
.item {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  border: 1px #000 solid;
  cursor: pointer;
  user-select: none;
  &:hover {
    background-color: #000;
    color: #fff;
  }
  &.active {
    background-color: #000;
    color: #fff;
  }
}
.selected-left {
  display: grid;
  gap: 6px;
  grid-template-columns: repeat(6, 1fr);
}
</style>
