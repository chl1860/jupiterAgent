<template>
<q-layout view="lHh Lpr lFf">
    <q-header elevated>
        <q-toolbar>
            <q-btn flat dense round icon="menu" aria-label="Menu" />
            <q-menu>
              <q-list style="min-width">
                <q-item clickable>
                  <q-item-section>Account</q-item-section>
                  <q-item-section side>
                    <q-icon name="keyboard_arrow_right"></q-icon>
                  </q-item-section>
                  <q-menu anchor="top right" self="top left">
                    <q-list>
                      <q-item clickable to="/account/relink">
                        <q-item-section>Re-map Prospect</q-item-section>
                      </q-item>
                      <q-item clickable to="/">
                        <q-item-section>To Prospect</q-item-section>
                      </q-item>
                    </q-list>
                  </q-menu>
                </q-item>
              </q-list>
            </q-menu>
            <q-toolbar-title>
                Jupiter Agent
            </q-toolbar-title>

            <div>{{loginAs}}</div>
        </q-toolbar>
    </q-header>

    <q-page-container>
        <router-view />
    </q-page-container>
</q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      loginAs: 'Seven Chen'
    }
  }
}
</script>
