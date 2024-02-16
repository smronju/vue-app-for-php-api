<template>
  <TheHeader />

  <div class="container">
    <ListSubscriber :subscribers="subscribers" :completed="completed"  @loadSubscriber="handleSubcriberLoad" @deleteSubscriber="handleSubscriberDelete" />
    <AddSubscriber @subscriberSubmitted="handleSubscriberSubmit" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useToast } from 'vue-toastification';
import TheHeader from './components/TheHeader.vue'
import ListSubscriber from './components/ListSubscriber.vue'
import AddSubscriber from './components/AddSubscriber.vue'

const toast = useToast();
const url = import.meta.env.VITE_API_ENDPOINT
let page = 1
let completed = ref(false)
let subscribers = ref([]);


onMounted (() => {
  fetch(`${url}?page=${page}`)
  .then(response => response.json())
  .then(json => {
    subscribers.value = json.data
  })
})

const handleSubcriberLoad = () => {
  page++

  fetch(`${url}?page=${page}`)
  .then(response => response.json())
  .then(json => {
    if (json.data.length === 0) {
      completed.value = true;
    }

    subscribers.value.push(...json.data);
  })
}

const handleSubscriberDelete = (id) => {
  fetch(`${url}/${id}`, { method: 'DELETE'})
  .then(response => {
    switch (response.status) {
      case 404:
        toast.error('Subscriber not found.');
        break;
      default:
        subscribers.value = subscribers.value.filter(subscriber => subscriber.id != id);
        toast.success('Subscriber deleted.');
        
        break;
    }
  });
}

const handleSubscriberSubmit = (subscriberData) => {
  let formData = new FormData();
  formData.append('first_name', subscriberData.first_name);
  formData.append('last_name', subscriberData.last_name);
  formData.append('email', subscriberData.email);
  formData.append('status', subscriberData.status);

  fetch(`${url}`, {method: 'POST', body: formData})
  .then(response => {
    if (response.status === 422) {
      toast.error('Please fill the required field.')
      return false;
    }

    if (response.status === 302) {
      toast.info('Subscriber already exists.');
      return false;
    }

    if (response.status === 201) {
      toast.success('Subscriber created.');
      return response.json();
    }
  })
}
</script>
