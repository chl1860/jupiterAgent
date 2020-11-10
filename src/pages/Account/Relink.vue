<template>
    <div class="q-pa-md">
      <q-btn label="Reset" push color="white" text-color="primary" @click="reset" class="q-mb-md" />
      <q-stepper
        v-model="step"
        header-nav
        ref="stepper"
        color="primary"
        keep-alive
        animated
      >
      <q-step
        :name="1"
        title="Put your account info"
        icon="settings"
        :done="done1"
        :header-nav="step > 1"
      >
       <div>
        <textarea name="" id="info" placeholder="Input your info here" :style ="{resize:'none'}" cols="30" rows="10" v-model="prospects"></textarea></div>
       <q-stepper-navigation>
          <q-btn @click="() => { done1 = true; step = 2 }" color="primary" label="Continue" />
        </q-stepper-navigation>
      </q-step>
      <q-step
        :name="2"
        title="Confirm your put info"
        icon="create_new_folder"
        :done="done2"
        :header-nav="step > 2"
      >
        <div class="q-pa-md">
          <q-table
            title="Prospect Info"
            :data="enteredProspects"
            :columns="columns"
            row-key="GCI_CLIENT_CODE"
            :filter="filter"
          >
            <template v-slot:top-right>
              <q-input borderless dense debounce="300" v-model="filter" placeholder="Search">
                <template v-slot:append>
                  <q-icon name="search" />
                </template>
              </q-input>
            </template>
          </q-table>
        </div>
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
          <q-btn color="primary" @click="save" label="Save" />
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
      filter: '',
      prospects: '',
      step: 1,
      done1: false,
      done2: false,
      done3: false,
      columns: [
        {
          name: 'GCI_CLIENT_CODE',
          required: true,
          label: 'GCI Code',
          align: 'left',
          field: 'GCI_CLIENT_CODE',
          sortable: true
        },
        {
          name: 'NEW_PROSPECT_ID',
          required: true,
          label: 'Survival Prospect',
          align: 'center',
          field: 'NEW_PROSPECT_ID',
          sortable: true
        },
        {
          name: 'OLD_PROSPECT_ID',
          required: true,
          label: 'Victim Prospect',
          align: 'center',
          field: 'OLD_PROSPECT_ID',
          sortable: true
        }
      ]
    }
  },
  computed: {
    enteredProspects () {
      var list = this.prospects.split(/(?:\n|\r\n)/g);
      return list.filter(o => o && o.length > 0).map((o) => {
        var array = o.split(/\t/g);
        return {
          GCI_CLIENT_CODE: `${array[2]}`,
          NEW_PROSPECT_ID: `${array[0]}`,
          OLD_PROSPECT_ID: `${array[1]}`
        };
      });
    }
  },

  methods: {
    reset () {
      this.done1 = false
      this.done2 = false
      this.done3 = false
      this.step = 1
      this.prospects = ''
    },
    save () {
      this.done3 = true
      console.log(this.enteredProspects);
    }
  }
}
</script>
