<script setup>
import contactsJson from '@/contacts.json'
import { ref, computed } from 'vue'
import { randomNumberFromAtoB } from '@/utilities.js'

const INITIAL_NUMBER_CONTACTS = 5

const contacts = ref([])

const contactsIndexes = ref([])

contacts.value = contactsJson.filter((contact, index) => index < INITIAL_NUMBER_CONTACTS)

//this will give the index of the contact to add and push it to the 
//contactsIndexes array to have it registered ...
const randomIndexOfRemaniningContacts = computed(() => {
  const max = contactsJson.length
  const min = contactsIndexes.value.length + 5
  let index = 0
  do {
    index = randomNumberFromAtoB(max, min)
  } while (contactsIndexes.value.includes(index))
  contactsIndexes.value.push(index)
  return index
})
const sortByName = () => {
  contacts.value.sort((a, b) => a.name.localeCompare(b.name))
}

const sortByPopularity = () => {
  contacts.value.sort((a, b) => b.popularity - a.popularity)
}
const addRandom = () => contacts.value.unshift(contactsJson[randomIndexOfRemaniningContacts.value])
</script>

<template>
  <div class="container">
    <h1>IronContacts</h1>
    <div class="buttons">
      <button @click="addRandom">Add Random Contact</button>
      <button @click="sortByName">Sort by name</button>
      <button @click="sortByPopularity">Sort by popularity</button>
    </div>
    <table>
      <th class="picture">
        <h2>Picture</h2>
      </th>
      <th class="name">
        <h2>Name</h2>
      </th>
      <th class="popularity">
        <h2>Popularity</h2>
      </th>
      <th>
        <h2>Won an Oscar</h2>
      </th>
      <th>
        <h2>Won an Emmy</h2>
      </th>
      <tr v-for="contact in contacts" :key="contact">
        <td><img :src="contact.pictureUrl" alt="artist picture"></td>
        <td>
          <h3>{{ contact.name }}</h3>
        </td>
        <td>
          <h3>{{ contact.popularity.toFixed(2) }}</h3>
        </td>
        <td><img v-if="contact.wonOscar" src="@/assets/trophy.svg" alt="trophy"></td>
        <td><img v-if="contact.wonEmmy" src="@/assets/trophy.svg" alt="trophy"></td>
      </tr>
    </table>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
}

h1 {
  font-size: 80px;
  text-align: center;
}

h2 {
  font-weight: bolder;
  font-size: 40px;
}

h3 {
  font-weight: 400;
  font-size: 30px;
}

td {
  text-align: center;
  width: 150px;
}

img {
  width: 110px;
}
.buttons {
  display: flex;
  align-self: center;
}
button {
  margin: 3px;
  width: 200px;
  height: 50px;
  background-color: aqua;
}
</style>
