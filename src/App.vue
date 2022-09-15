<template>
  <main-page></main-page>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import MainPage from './components/MainPage.vue';

@Options({
  components: {
    MainPage,
  },
})
export default class App extends Vue {}
</script>

<style>
</style>
