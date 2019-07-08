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
            <div class="col-6" v-for="item in optionList" :key="item.val">
              <q-checkbox v-model="optionsNpm" :val="item.val" :label="item.label" />
            </div>
          </div>
        </q-card-section>
      </q-card>
      <div>
        <q-btn label="Submit" type="submit" color="primary" />
      </div>
      {{optionsNpm}}
    </q-form>
  </div>
</template>

<script>
const formSetting = [
  {
    type: 'npm',
    data: [
      { val: 'deps', label: 'deps' },
      { val: 'devDeps', label: 'devDeps' },
      { val: 'peerDeps', label: 'peerDeps' },
      { val: 'yarn.lock', label: 'yarn.lock' },
      { val: 'package-lock.json', label: 'package-lock.json' },
    ],
  }, {
    type: 'node',
    data: [
      { val: '.nvmrc', label: '.nvmrc' },
      { val: 'package.json', label: 'package.json' },
      { val: 'engince', label: 'engince' },
    ],
  },
];

export default {
  name: 'main-form',
  data() {
    return {
      type: 'npm',
      pkgVersion: '',
      optionsNpm: [],
    };
  },
  computed: {
    isNode() {
      return this.type === 'node';
    },
    optionList() {
      const setting = formSetting.find(t => t.type === this.type);

      return setting ? setting.data : [];
    },
  },
  methods: {
    pkgVersionRule(val) {
      if (this.isNode) {
        return true;
      }

      return val && val.length > 0;
    },
    onSubmit() {
      console.log(`type - ${this.type}`);
      console.log(`pkgVersion - ${this.pkgVersion}`);
      console.log(`optionsNpm - ${this.optionsNpm}`);
    },
  },
  watch: {
    type() {
      this.optionsNpm = [];
      this.pkgVersion = '';
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
