<style>
.table {
  border: 0.05rem solid var(--box-border);
  box-shadow: 1px 1px 30px var(--box-shadow);
  width: max-content;
  margin: auto;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  width: max-content;
}

.table-body-cell,
.table-header-cell {
  width: 100%;
  min-width: 12rem;
  border: 0.05rem solid var(--box-border);
  height: 2.8rem;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.table-header-cell {
  width: 100%;
  font-weight: bold;
  background-color: aliceblue;
  color: rgb(77, 81, 82);
  border-top: none;
}

.table-header-cell:first-child {
  border-left: none;
}

.table-header-cell:last-child {
  border-right: none;
}

.colors {
  height: 100%;
  width: max-content;
  position: relative;
  left: 0;
  display: flex;
  background-color: aqua;
}

.color {
  width: 1rem;
}

.table-body-cell-colored {
  display: flex;
  justify-content: space-between;
  padding-right: 1rem;
  gap: 2rem;
}
</style>

<template>
  <div class="table">
    <div
      class="table-header-cell"
      v-for="header in tableHeader"
      :key="header.id"
    >
      {{ header.title }}
    </div>

    <template v-for="(row, index1) in tableBody">
      <div
        v-for="(cell, key, index) in row"
        v-bind:class="
          !index ? 'table-body-cell table-body-cell-colored' : 'table-body-cell'
        "
        :key="cell.id"
        v-if="!hiddenParameters.includes(key)"
      >
        <div v-if="!index" class="colors">
          <div
            v-for="chain in nestedChains[index1]"
            :key="chain.id"
            class="color"
            :style="{ backgroundColor: chain.color }"
          ></div>
        </div>

        <div>{{ cell }}</div>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'AppTable',
  props: {
    tableHeader: {
      type: Array
    },
    tableBody: {
      type: Array
    },
    hiddenParameters: {
      type: Array
    }
  },
  computed: {
    nestedChains () {
      return this.tableBody.map((search) => {
        let nestedChain = []
        nestedChain.push(search)

        while (search.parentId) {
          search = this.tableBody.find((item) => search.parentId === item.id)
          nestedChain.push(search)
        }
        return nestedChain.reverse()
      })
    }
  }
}
</script>
