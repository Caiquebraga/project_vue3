<template>
  <div>
    <header>
      <img
        alt="Vue logo"
        class="logo"
        src="@/assets/logo.svg"
        width="125"
        height="125"
      />

      <div class="wrapper">
        <HelloWorld msg="You did it!" />

          {{count}}

          {{UserNAme}}

          <ul>
            <li v-for="user in users" :key="user.id">{{user.FistName}} - {{user.age}}</li>
          </ul>

        <button v-on:click="count++">Add</button>

        <nav>
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/products">products</RouterLink>
          <RouterLink to="/about">About</RouterLink>
        </nav>
      </div>
    </header>

    <Footer></Footer>

    <RouterView />
  </div>
</template>

<script setup>
import { onMounted, onUpdated, reactive, ref } from "vue";

import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "@/components/HelloWorld.vue";
import Footer from "@/components/Footer.vue";


const count = ref(0);

const UserNAme = ref("Caique");

const users = reactive([
  {
    FistName:'caique',
    age:29
  },
{
  FistName: 'Paula',
  age: 24
}
])

onMounted( () => {
  console.log('Monunted');
})

onUpdated( () =>{
    console.log('onUpdated');
})


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
