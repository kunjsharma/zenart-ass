<template>
  <XHeader/>
  <XPost/>
</template>

<script>
import XPost from './components/XPost.vue';
import XHeader from './components/XHeader.vue';

export default {
  name: 'App',
  components: {
    XHeader,
    XPost
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  margin-top: 60px;
  background-color: #000000;
  width: 50%;
  margin: 0 auto;
}
</style>
