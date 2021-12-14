<template>
  <div id="app">
    <Users />
  </div>
</template>

<script>


import Users from '../src/components/Users.vue';

export default {
  name: 'App',
  components: {
    Users,
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
</style>
