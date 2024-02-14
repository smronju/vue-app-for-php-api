<template>
  <Header />

  <div class="container">
    <ListSubscriber :subscribers="subscribers" />
    <AddSubscriber />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Header from './components/Header.vue'
import ListSubscriber from './components/ListSubscriber.vue'
import AddSubscriber from './components/AddSubscriber.vue'

const subscribers = ref([
  {
    id: 1,
    first_name: 'John',
    last_name: 'Doe',
    email: 'johndoe@mailinator.com',
    status: 0
  },
  {
    id: 2,
    first_name: 'Jane',
    last_name: 'Doe',
    email: 'janedoe@mailinator.com',
    status: 1
  },
  {
    id: 3,
    first_name: 'John',
    last_name: 'Smith',
    email: 'johnsmith@mailinator.com',
    status: 0
  },
  {
    id: 4,
    first_name: 'Jenny',
    last_name: 'Doe',
    email: 'jennydoe@mailinator.com',
    status: 0
  },
  {
    id: 5,
    first_name: 'Johny',
    last_name: 'Doe',
    email: 'johnydoe@mailinator.com',
    status: 1
  }
])
</script>
