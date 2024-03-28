<script setup>
import contactsJson from '@/contacts.json'
import { ref, computed } from 'vue'
import { randomNumberFromAtoB } from '@/utilities.js'

const INITIAL_NUMBER_CONTACTS = 5

const contacts = ref([])

const contactsIndexes = ref([])

contacts.value = contactsJson.filter((contact, index) => index < INITIAL_NUMBER_CONTACTS)

//this will give the index of the contact to add
const randomIndexOfRemaniningContacts = computed(() => {
  const max = contactsJson.length
  const min = contactsIndexes.value.length
  let index = 0
  do {
    index = randomNumberFromAtoB(max, min)
  } while (contactsIndexes.value.includes(index))
  contactsIndexes.value.push(index)
  return index
})
const addRandom = () => contacts.value.unshift(contactsJson[randomIndexOfRemaniningContacts.value])
</script>

<template>
  <div class="container">
    <h1>IronContacts</h1>
    <button @click="addRandom">Add Random</button>
    <table>
      <th class="picture"><h2>Picture</h2></th>
      <th class="name">
        <h2>Name</h2>
      </th>
      <th class="popularity">
        <h2>Popularity</h2>
      </th>
      <th><h2>Won an Oscar</h2></th>
      <th><h2>Won an Emmy</h2></th>
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
  font-weight:bolder;
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
button {
  width: 200px;
  height: 50px;
  align-self: center;
  background-color: aqua;
}
</style>
