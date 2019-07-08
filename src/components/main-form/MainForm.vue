<template>
  <div class="q-pa-md">
    <q-form @submit="onSubmit" class="q-gutter-md">
      <div class="text-h2">Search</div>
      <div class="row">
        <div class="col flex items-center">
          <q-radio v-model="type" val="npm" label="NPM package version" />
        </div>
        <div class="col">
          <q-input
            v-model="pkgVersion"
            label="Version"
            :rules="[ (val) => pkgVersionRule(val) || 'Please type something']"
            :disable="isNode"
          />
        </div>
      </div>
      <div class="row">
        <div class="col">
          <q-radio v-model="type" val="node" label="Node version" />
        </div>
      </div>
      <q-card bordered>
        <q-card-section>
          <div class="text-h6">Options</div>
        </q-card-section>
        <q-separator inset />
        <q-card-section>
          <div class="row">
            <div class="col">
              asds
            </div>
          </div>
        </q-card-section>
      </q-card>
      <div>
        <q-btn label="Submit" type="submit" color="primary" />
      </div>
    </q-form>
  </div>
</template>

<script>
export default {
  name: 'main-form',
  data() {
    return {
      type: 'npm',
      pkgVersion: '',
      a: 12,
    };
  },
  computed: {
    isNode() {
      return this.type === 'node';
    },
  },
  methods: {
    pkgVersionRule(val) {
      if (this.isNode) {
        return true;
      }
      console.log('testRule');
      console.log(this.isNode);
      return val && val.length > 0;
    },
    onSubmit() {
      console.log('onSubmit');
    },
  },
};
</script>

<style>
.q-pa-md {
  width: 100%;
  max-width: 500px;
}
</style>
