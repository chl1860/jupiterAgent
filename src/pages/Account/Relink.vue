<template>
    <div class="q-pa-md">
      <q-btn label="Reset" push color="white" text-color="primary" @click="reset" class="q-mb-md" />
      <q-stepper
        v-model="step"
        header-nav
        ref="stepper"
        color="primary"
        animated
      >
      <q-step
        name="1"
        title="Put your account info"
        icon="settings"
        :done="done1"
      >
        <textarea name="" id="" cols="30" rows="10" v-model="prospects"></textarea>

       <q-stepper-navigation>
          <q-btn @click="() => { done1 = true; step = 2 }" color="primary" label="Continue" />
        </q-stepper-navigation>
      </q-step>
      <q-step
        :name="2"
        title="Confirm your put info"
        icon="create_new_folder"
        :done="done2"
      >
        info to confirm
        <div>{{prospects.split(/(?:\n|\n\r)/g)}}</div>
        <q-stepper-navigation>
          <q-btn @click="() => { done2 = true; step = 3 }" color="primary" label="Continue" />
          <q-btn flat @click="step = 1" color="primary" label="Back" class="q-ml-sm" />
        </q-stepper-navigation>
      </q-step>
      <q-step
        :name="3"
        title="Save new prospect info"
        icon="add_comment"
        :done="done3"
      >
      Finish
      <q-stepper-navigation>
          <q-btn color="primary" @click="done3 = true" label="Finish" />
          <q-btn flat @click="step = 2" color="primary" label="Back" class="q-ml-sm" />
        </q-stepper-navigation>
      </q-step>
      </q-stepper>
    </div>
</template>
<script>
export default {
  name: 'AccountRelink',
  data () {
    return {
      title: 'Account Relink Page',
      prospects: '',
      step: 1,
      done1: false,
      done2: false,
      done3: false
    }
  },
  methods: {
    reset () {
      this.done1 = false
      this.done2 = false
      this.done3 = false
      this.step = 1
    }
  }
}
</script>
