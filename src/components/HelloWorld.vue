<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<script>
export default
{
  data(){
    return{
      holderAdd: 'Введите название',
      holderSearch: 'Введите для поиска',
      inputValueAdd: '',
      inputValueSearch: '',
      notes: ['Test1', 'Test2', 'Test3', 'q'],
      notesSerch: []
    }
  },

  methods:{
        addNewNote(){
            this.notes.push(this.inputValueAdd)
            this.inputValueAdd = ''
        },

        searchNotes(event){
            this.inputValueSearch = event.target.value
            this.notesSerch = this.notes.filter(el => el.match(this.inputValueSearch))
        }
  }
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <div class="form-add">
    <input 
      type="text" 
      v-bind:placeholder="holderAdd"
      v-model="inputValueAdd"
    />
    <button class="btn" v-on:click="addNewNote">Добавить</button>
  </div>
  <div class="form-search">
    <input 
      type="text"
      v-bind:placeholder="holderSearch"
      v-on:input="searchNotes"
      v-on:keypress="searchNotes"
    />
  </div>
  <hr />
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
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
