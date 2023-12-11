<script setup>
import { ref, watch } from 'vue'

const holderAdd = 'Введите название'
const holderSearch = 'Введите для поиска'


const inputValueAdd = ref('')
const inputValueSearch = ref('')
const notes = ref(['Test1', 'Test2', 'Test3', 'q'])
const notesSerch = ref([])

const addNewNote = () => {
  notes.value.push(inputValueAdd.value)
  inputValueAdd.value = ''
}

watch (inputValueSearch, (nv) => {
  inputValueSearch.value = nv
  notesSerch.value = notes.value.filter(el => el.match(inputValueSearch.value))
})

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
      v-model="inputValueAdd"
    />
    <button class="btn" v-on:click = "addNewNote">Добавить</button>
  </div>
  <div class="form-search">
    <input 
      type="text"
      v-bind:placeholder="holderSearch"
      v-model="inputValueSearch"
    />
  </div>
  <hr />
  <div>
    <ul class="list" v-if="inputValueSearch.length !== 0">
    <li class="list-item" v-for="note of notesSerch">
      {{ note }}
    </li>
  </ul>
    <ul class="list" v-else>
    <li class="list-item" v-for="note of notes">
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
