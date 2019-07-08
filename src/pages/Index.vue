<template>
  <q-page class="flex justify-center">
    <main-form />
  </q-page>
</template>

<style>
</style>

<script>
import MainFormVue from '../components/main-form/MainForm.vue';


export default {
  components: {
    'main-form': MainFormVue,
  },
  name: 'PageIndex',
};
</script>
