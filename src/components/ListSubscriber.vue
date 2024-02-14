<template>
  <h3>Subscriber List</h3>
  <ul id="list" class="list">
    <li
      v-for="subscriber in subscribers"
      :key="subscriber.id"
      :class="subscriber.status === 0 ? 'inactive' : 'active'"
    >
      {{ subscriber.first_name }}{{ subscriber.last_name }} <span>{{ subscriber.email }}</span>
      {{ subscriber.status === 0 ? 'Inactive' : 'Active' }}
      <button class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  subscribers: {
    type: Array,
    required: true
  }
})
</script>
