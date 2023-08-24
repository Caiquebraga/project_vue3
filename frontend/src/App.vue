<template>
  <div>
    
      <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

      <div class="wrapper">
        
          <Header v-if="showHeader"></Header>
       
          <h2>users list</h2>
          
          <ul>
            <li v-for="user in users" :key="user.id">
             {{ user.firstName }} 
             <button style="background-color: rgb(255, 42, 14);" v-if="user.is_admin">  admin</button>
             <button style="background-color: aquamarine;" v-else="user.is_admin"> not admin</button>
            </li>
          </ul>

        <nav>
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/products">products</RouterLink>
          <RouterLink to="/about">About</RouterLink>
        </nav>
      </div>

    <Footer></Footer>

    <RouterView />
  </div>
</template>

<script setup>
import { onMounted, onUpdated, reactive, ref } from "vue";

import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "@/components/HelloWorld.vue";
import Footer from "@/components/Footer.vue";
import http from '@/services/http.js';
import Header from '@/components/Header.vue';


const users = reactive([] );

let showHeader = false;

const fetchData = async () => {
  try {
    const { data } = await http.get('/api/users');
    users.length = 0; // Limpar o array reativo
    users.push(...data); // Atualizar o array com os dados obtidos
  } catch (error) {
    console.log(error);
  }
};

onMounted(fetchData);
</script>


<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
