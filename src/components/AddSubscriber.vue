<template>
  <h3>New Subscriber</h3>

  <form id="form" @submit-prevent="onSubmit">
    <div class="form-control">
      <label for="firstName">First Name</label>
      <input type="text" id="firstName" placeholder="First name" />
    </div>

    <div class="form-control">
      <label for="lastName">Last Name</label>
      <input type="text" id="lastName" placeholder="Last name" />
    </div>

    <div class="form-control">
      <label for="email">Email</label>
      <input type="text" id="email" placeholder="Email address" />
    </div>

    <div class="form-control">
      <label for="status">Status</label>
      <select name="status">
        <option value="1">Active</option>
        <option value="0">Inactive</option>
      </select>
    </div>

    <button class="btn">Add Subscriber</button>
  </form>
</template>

<script setup>
const onSubmit = () => {
  console.log('submit')
}
</script>
