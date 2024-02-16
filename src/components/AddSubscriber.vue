<template>
  <h3>New Subscriber</h3>

  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="firstName">First Name *</label>
      <input type="text" id="firstName" v-model="firstName" placeholder="First name" />
    </div>

    <div class="form-control">
      <label for="lastName">Last Name *</label>
      <input type="text" id="lastName" v-model="lastName" placeholder="Last name" />
    </div>

    <div class="form-control">
      <label for="email">Email *</label>
      <input type="text" id="email" v-model="email" placeholder="Email address" />
    </div>

    <div class="form-control">
      <label for="status">Status</label>
      <select name="status" v-model="status">
        <option value="1">Active</option>
        <option value="0">Inactive</option>
      </select>
    </div>

    <button class="btn">Add Subscriber</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const firstName = ref('');
const lastName = ref('');
const email = ref('');
const status = ref(1);

const toast = useToast();
const emit = defineEmits(['subscriberSubmitted']);

const onSubmit = () => {
  if (!firstName.value || !lastName.value || !email.value) {
    toast.error('Please fill the required field.');

    return false;
  }

  const subscriberData = {
    first_name: firstName.value,
    last_name: lastName.value,
    email: email.value,
    status: parseInt(status.value)
  }

  emit('subscriberSubmitted', subscriberData);

  firstName.value = '';
  lastName.value = '';
  email.value = '';
  status.value = 1;
}
</script>
