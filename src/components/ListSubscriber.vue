<template>
  <h3>Subscriber List</h3>
  <ul id="list" class="list" v-if="subscribers.length">
    <li
      v-for="subscriber in subscribers"
      :key="subscriber.id"
      :class="subscriber.status === 0 ? 'inactive' : 'active'"
    >
      {{ subscriber.first_name }} {{ subscriber.last_name }} <span>{{ subscriber.email }}</span>
      {{ subscriber.status === 0 ? 'Inactive' : 'Active' }}
      <button class="delete-btn" @click="deleteSubscriber(subscriber.id)">x</button>
    </li>
  </ul>

  <p v-else>{{ subscribers.length == 0 ? 'Create subscriber' : 'Loading...' }}</p>

  <button class="btn" v-show="subscribers.length" @click="loadSubscriber">{{ completed ? 'All Loaded' : 'Load More...' }}</button>
</template>

<script setup>
const emit = defineEmits(['loadSubscriber', 'deleteSubscriber']);

const loadSubscriber = () => {
  emit('loadSubscriber');
}

const deleteSubscriber = (id) => {
  emit('deleteSubscriber', id)
}

defineProps({
  subscribers: {
    type: Array,
    required: true
  },
  completed: {
    type: Boolean,
    required: true
  }
})
</script>
