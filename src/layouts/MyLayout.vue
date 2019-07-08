<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title>Github Repo Tools</q-toolbar-title>
        <q-item
          tag="a"
          href="https://github.com/lightness/github-repo-tools"
          target="_blank"
          class="items-center"
        >
          <q-icon name="fab fa-github" />
        </q-item>
      </q-toolbar>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar';

export default {
  name: 'MyLayout',
  data() {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop,
    };
  },
  methods: {
    openURL,
  },
};
</script>

<style>
</style>
