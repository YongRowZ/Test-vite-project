<script setup>
import { reactive } from 'vue'

const holderAdd = 'Введите название'
const holderSearch = 'Введите для поиска'

const data = reactive({
  inputValueAdd: '',
  inputValueSearch: '',
  notes: ['Test1', 'Test2', 'Test3', 'q'],
  notesSerch: []
})

const addNewNote = () => {
  data.notes.push(data.inputValueAdd)
  data.inputValueAdd = ''
}

const searchNotes = () => {
  data.notesSerch = data.notes.filter(el => el.match(data.inputValueSearch))
}

defineProps({
  msg: String,
})

</script>

<template>
  <h1>{{ msg }}</h1>
  <div class="form-add">
    <input 
      type="text"
      v-bind:placeholder = "holderAdd"
      v-model = data.inputValueAdd
    />
    <button class="btn" v-on:click = "addNewNote">Добавить</button>
  </div>
  <div class="form-search">
    <input 
      type="text"
      v-bind:placeholder="holderSearch"
      v-model="data.inputValueSearch"
      v-on:input="searchNotes"
      v-on:keypress="searchNotes"
    />
  </div>
  <hr />
  <div>
    <ul class="list" v-if="data.inputValueSearch.length !== 0">
    <li class="list-item" v-for="note of data.notesSerch">
      {{ note }}
    </li>
  </ul>
    <ul class="list" v-else>
    <li class="list-item" v-for="note of data.notes">
      {{ note }}
    </li>
  </ul>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
