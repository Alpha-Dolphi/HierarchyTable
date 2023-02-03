<style>
.form {
  border-radius: 1rem;
  padding: 1.2rem;
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  align-items: center;
  position: fixed;
  width: 28rem;
  height: max-content;
  right: calc(50% - 13rem);
  top: 25%;
  background: var(--prime-light-color);
  border: 0.05rem solid var(--box-border);
  box-shadow: 1px 1px 30px var(--box-shadow);
}

.data-input-section {
  display: flex;
  gap: 0.8rem;
  flex-direction: column;
  width: 90%;
}

.data-input {
  display: grid;
  grid-template-columns: 1fr 1fr;
  justify-content: space-between;
  gap: 0.8rem;
}

.data-input input,
.data-input select {
  border: 0.05rem solid #9a9d9f;
  width: 12rem;
  border-radius: 0.3rem;
  padding: 5px;
  padding-top: 2px;
  padding-bottom: 2px;
  height: 1.6rem;
}

.data-input input:focus,
.data-input select:focus {
  outline: 3px solid var(--input-outline);
  -moz-outline-radius: 1px;
  box-shadow: 0px 0px 15px var(--input-outline);
}

.main-input input {
  margin-right: -0.76rem;
}

.in-form {
  margin-top: 1rem;
  width: 100%;
  box-shadow: none;
  background-color: rgb(165, 201, 242);
}

.in-form:hover {
  scale: 1.015;
}

hr {
  width: 100%;
  height: 0.03rem;
  background-color: var(--box-border);
  border: 0.03rem solid var(--box-border);
  border-radius: 0.03rem;
  grid-column: 1/4;
}

.hint {
  font-size: 0.8rem;
}
</style>

<template>
  <form class="form" v-on:submit.prevent="onSubmit">
    <h2>New User</h2>

    <hr/>

    <div class="data-input-section">
      <div
        class="data-input main-input"
        v-for="(item, index) in tableHeader"
        :key="item.id"
      >
        <div>
          <p>{{ item.title }}</p>

          <p v-if="item.title === 'Phone number'" class="hint">
            {{ item.title === "Phone number" ? "(+7 985 198 56 77)" : "" }}
          </p>
        </div>

        <input
          v-if="item.inputType === 'tel'"
          type="tel"
          pattern="^\+7\s\d{3}\s\d{3}\s\d{2}\s\d{2}$"
          v-model="values[index]"
          required
        />

        <input
          v-else
          :type="item.inputType"
          min="16"
          v-model="values[index]"
          required
        />

        <hr />
      </div>

      <div class="data-input">
        <p>Supervisor</p>

        <select v-model="supervisorInput">
          <option v-bind:value="missing">—</option>

          <option
            v-for="(item, index) in tableBody"
            :key="index"
            v-bind:value="item.id"
          >
            {{ item.name }}
          </option>
        </select>
      </div>

      <button class="form-button in-form">Save</button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'AppForm',
  props: {
    tableHeader: {
      type: Array
    },
    tableBody: {
      type: Array
    }
  },
  data () {
    return {
      values: [],
      supervisorInput: '',
      missing: ''
    }
  },
  methods: {
    onSubmit () {
      this.addNewUser()
      this.saveToLocalStorage()
      this.hideForm()
    },
    addNewUser () {
      const newUser = {}
      this.tableHeader.forEach((item, index) => {
        newUser[item.id] = this.values[index]
      })
      newUser.color = '#' + Math.floor(Math.random() * 16777215).toString(16)
      newUser.id = Math.random()
      newUser.parentId = this.supervisorInput
      this.$emit('submit', newUser)
    },
    saveToLocalStorage () {
      localStorage.setItem('array', JSON.stringify(this.tableBody))
    },
    hideForm () {
      this.$emit('hideForm')
    }
  }
}
</script>
