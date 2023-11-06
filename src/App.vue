<script setup>
  import { ref } from 'vue';
  import store from './store/index';
  import supabase from './supabase/init';
  import Navigation from './components/Navigation.vue';

  const appReady = ref(null)
  const user = supabase.auth.user()

  if(!user){
    appReady.value = true
  }

  supabase.auth.onAuthStateChange((_, session) => {
    store.methods.setUser(session)
    appReady.value = true
  })
</script>

<template>
  <div v-if="appReady" class="min-h-full font-Poppins box-border">
    <Navigation/>
    <router-view />
  </div>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700&display=swap");
</style>
