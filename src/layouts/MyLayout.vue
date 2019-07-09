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
import querystring from 'querystring';
import axios from 'axios';

const GITHUB_CLIENT_ID = '8b20e17f2c8c05c29536';
const GITHUB_AUTH_URL = 'https://github.com/login/oauth/authorize';
const GET_TOKEN_URL = 'http://localhost:3000/api/token';
const REDIRECT_URL = window.location.origin;
const SCOPE = 'repo';
const LS_KEY = 'token';

function navigateToGithubAuth() {
  const query = {
    client_id: GITHUB_CLIENT_ID,
    redirect_uri: REDIRECT_URL,
    scope: SCOPE,
  };
  const queryStr = querystring.stringify(query);

  window.location.href = `${GITHUB_AUTH_URL}?${queryStr}`;
}

if (window.location.search.indexOf('code=') > -1) {
  const { code, ...rest } = querystring.parse(window.location.search.slice(1));

  axios({
    method: 'post',
    url: GET_TOKEN_URL,
    data: {
      code,
    },
  })
    .then((response) => {
      localStorage.setItem(LS_KEY, JSON.stringify(response.data));
      window.location.search = querystring.stringify(rest);
    })
    .catch((err) => {
      console.error(err);
    });
} else {
  const token = localStorage.getItem(LS_KEY);
  if (!token) {
    navigateToGithubAuth();
  }
}

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
