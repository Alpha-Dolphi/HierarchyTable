<style>
.content {
  display: grid;
  padding: 2rem;
  gap: 1.1rem;
}

.form-button {
  width: 8rem;
  height: 2.2rem;
  border-radius: 0.5rem;
  margin: auto;
  font-size: 1.2rem;
  font-weight: bold;
  border: 0.05rem solid var(--box-border);
  background-color: rgb(165, 201, 242);
  color: var(--prime-light-color);
  transition: 0.28s;
  cursor: pointer;
}

.form-button:hover {
  background-color: rgb(39, 216, 151);
  scale: 1.05;
}
</style>

<template>
  <div class="content">
    <button class="form-button" v-on:click="showForm = !showForm">Add</button>

    <AppTable
      :tableHeader="tableHeader"
      :tableBody="tableBody"
      :hiddenParameters="hiddenParameters"
    />

    <AppForm
      v-if="showForm"
      :tableHeader="tableHeader"
      :tableBody="tableBody"
      @submit="tableBody.push($event)"
      @hideForm="showForm = !showForm"
    />
  </div>
</template>

<script>
import AppTable from './AppTable.vue'
import AppForm from './AppForm.vue'

export default {
  name: 'AppLayout',
  components: {
    AppTable,
    AppForm
  },
  data () {
    return {
      showForm: false,
      tableHeader: [
        {
          id: 'name',
          title: 'Name',
          sortable: true,
          sortType: { type: String },
          inputType: 'text'
        },
        {
          id: 'phone',
          title: 'Phone number',
          sortable: false,
          sortType: { type: String },
          inputType: 'tel'
        },
        {
          id: 'age',
          title: 'Age',
          sortable: true,
          sortType: { type: Number },
          inputType: 'number'
        }
      ],
      tableBody: [
        {
          name: 'Marina',
          phone: '+7 985 198 56 18',
          age: 21,
          color: '#' + Math.floor(Math.random() * 16777215).toString(16),
          parentId: 989,
          id: 999
        },
        {
          name: 'Petr',
          phone: '+7 985 500 56 20',
          age: 24,
          color: '#' + Math.floor(Math.random() * 16777215).toString(16),
          parentId: 999,
          id: Math.random()
        },
        {
          name: 'Alexey',
          phone: '+7 800 555 35 35',
          age: 34,
          color: '#' + Math.floor(Math.random() * 16777215).toString(16),
          parentId: null,
          id: 989
        },
        {
          name: 'Boris',
          phone: '+7 985 198 88 13',
          age: 19,
          color: '#' + Math.floor(Math.random() * 16777215).toString(16),
          parentId: null,
          id: Math.random()
        }
      ],
      hiddenParameters: ['color', 'parentId', 'id']
    }
  },
  mounted () {
    // const arrayString = localStorage.getItem('array')
    // if (arrayString) {
    //   const array = JSON.parse(arrayString)
    //   this.tableBody = array
    // }
  }
}
</script>
