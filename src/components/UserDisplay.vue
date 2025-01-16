<template>
  <div class="main-container">
    <div class="section">
      <h2 class="section-title">Posts</h2>
      <ul class="list">
        <li v-for="post in posts" :key="post.id" class="list-item">
          <h3 class="item-title">{{ post.title }}</h3>
          <p class="item-content">{{ post.body }}</p>
        </li>
      </ul>
    </div>

    <div class="section">
      <h2 class="section-title">Users</h2>
      <button @click="fetchUsers" class="button">Reload Users</button>
      <ul class="list">
        <li v-for="user in users" :key="user.id" class="list-item">
          <h3 class="item-title">{{ user.name }}</h3>
          <p class="item-content">Email: {{ user.email }}</p>
          <p v-if="user.website" class="item-content">Website: <a :href="'http://' + user.website" target="_blank" rel="noopener noreferrer">{{ user.website }}</a></p>
          <p v-else class="item-content">Website: Not available</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserDisplay  ",
  data() {
    return {
      posts: [],
      users: [],
    };
  },
  methods: {
    async fetchPosts() {
      try {
        const response = await fetch("https://jsonplaceholder.typicode.com/posts");
        this.posts = await response.json();
      } catch (error) {
        console.error("Error fetching posts:", error);
      }
    },
    async fetchUsers() {
      try {
        const response = await fetch("https://jsonplaceholder.typicode.com/users");
        this.users = await response.json();
      } catch (error) {
        console.error("Error fetching users:", error);
      }
    },
  },
  created() {
    this.fetchPosts();
    this.fetchUsers();
  },
};
</script>

<style scoped>
.main-container {
  display: flex;
  flex-direction: column;
  gap: 30px;
  padding: 20px;
  background-color: #eef2f7;
  font-family: 'Arial', sans-serif;
}

.section {
  background: #ffffff;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.section-title {
  font-size: 24px;
  color: #2c3e50;
  margin-bottom: 20px;
  text-align: center;
}

.list {
  list-style: none;
  margin: 0;
  padding: 0;
}

.list-item {
  padding: 15px;
  margin-bottom: 15px;
  border: 1px solid #dcdcdc;
  border-radius: 8px;
  background: #f9f9f9;
  transition: background-color 0.3s;
}

.list-item:hover {
  background-color: #f1f7ff;
}

.item-title {
  font-size: 18px;
  color: #34495e;
  margin-bottom: 10px;
}

.item-content {
  font-size: 14px;
  color: #7f8c8d;
}

.button {
  display: block;
  margin: 0 auto 20px;
  padding: 10px 20px;
  font-size: 16px;
  color: #ffffff;
  background-color: #3498db;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.button:hover {
  background-color: #2980b9;
}
</style>
