<script setup>
import { ref } from 'vue';
import CommentSection from './components/CommentSection.vue';

const userId = ref('');
const users = ref([]);
const newEmail = ref('');

const getUser = async () => {
  try {
    const response = await fetch(`http://localhost:3000/api/user/${userId.value}`);
    if (response.ok) {
      users.value = await response.json();
    } else {
      console.error('Failed to fetch user data');
    }
  } catch (error) {
    console.error('Error fetching user:', error);
  }
};

const changeEmail = async () => {
  try {
    await fetch('http://localhost:3000/api/change-email', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ email: newEmail.value }),
    });
  } catch (error) {
    console.error('Error changing email:', error);
  }
};
</script>

<template>
  <div id="app">
    <h1>User Dashboard</h1>
    <div>
      <input v-model="userId" placeholder="Enter User ID" />
      <button @click="getUser">Get User Info</button>
    </div>
    <div v-if="users.length">
      <div v-for="(user, index) in users" :key="index">
        <h2>{{ user.name }}</h2>
        <p>Email: {{ user.email }}</p>
        <hr />
      </div>
    </div>
    <CommentSection />
    <form @submit.prevent="changeEmail">
      <h3>Change Email</h3>
      <input v-model="newEmail" placeholder="New Email" />
      <button type="submit">Submit</button>
    </form>
  </div>
</template>
