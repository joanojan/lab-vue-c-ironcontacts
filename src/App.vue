<script setup>
import contactsJson from '@/contacts.json'
import ContactsTable from '@/components/ContactsTable.vue'
import { ref, provide } from 'vue'

const contacts = ref([])

contacts.value = contactsJson.filter((contact, index) => index < 5)

provide('contacts', contacts)
</script>

<template>
  <div class="container">
    <h1>IronContacts</h1>
    <table>
      <th class="picture"><h2>Picture</h2></th>
      <th class="name">
        <h2>Name</h2>
      </th>
      <th class="popularity">
        <h2>Popularity</h2>
      </th>
      <tr v-for="contact in contacts" :key="contact">
        <td><img :src="contact.pictureUrl" alt="artist picture"></td>
        <td>
          <h3>{{ contact.name }}</h3>
        </td>
        <td>
          <h3>{{ contact.popularity.toFixed(2) }}</h3>
        </td>
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
</style>
