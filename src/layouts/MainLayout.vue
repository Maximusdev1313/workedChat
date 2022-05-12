<template>
  <q-layout view="lHr lpR fFf">
<!-- this is header -->
    <q-header
      elevated
      class="bg-white text-dark">
      <q-toolbar>
       <q-btn
        danse
        flat
        round
        icon="menu"
        @click="toggleLeftDrawer"
        ></q-btn>

        <q-toolbar-title
          class="text-weight-bold gt-sm "
          >

            {{$route.name}}
        </q-toolbar-title>
        <q-icon
          name="forum"
          size="sm"
          class="q-pa-md lt-md absolute-center"
          color="primary"

      > </q-icon>
      </q-toolbar>
    </q-header>
<!-- this is left drawer -->
    <q-drawer
      v-model="leftDrawerOpen"
      side="left"
      bordered
      class="absolute"
      >

      <!-- for icon -->
      <span class="row justify-between items-center">
         <q-icon name="fas fa-dove"
            size="lg"
            class="q-pa-lg "
            color="primary"

      > </q-icon>
      <q-icon
        name="fa fa-arrow-left"
        size="sm"
        class="q-mr-md lt-md"
        @click="toggleLeftDrawer"
        rounded
        clickable
      >
      </q-icon>
      </span>

      <q-list >
          <q-item
            clickable
            v-ripple
            to="/"
            exact
            >
              <q-item-section avatar>
                 <q-icon
                    name="home"
                    size="md" />
              </q-item-section>
              <q-item-section
                  class="text-weight-bold">Home
              </q-item-section>
          </q-item>
          <!-- <q-item
            exact
            clickable
            v-ripple
            to="/about">
            <q-item-section
                avatar>
                 <q-icon
                    name="help"
                    size="md" />
              </q-item-section>
              <q-item-section
                class="text-weight-bold">About
              </q-item-section>

          </q-item> -->
           <!-- <q-item
            clickable
            v-ripple
            to="/signin"
            exact
            >
              <q-item-section avatar>
                 <q-icon
                    name="login"
                    size="md" />
              </q-item-section>
              <q-item-section
                  class="text-weight-bold">
                  SignIn
              </q-item-section>
          </q-item>
            <q-item
            clickable
            v-ripple
            to="/register"
            exact
            >
              <q-item-section avatar>
                 <q-icon
                    name="person_add"
                    size="md" />
              </q-item-section>
              <q-item-section
                  class="text-weight-bold">
                  Register
              </q-item-section> 
          </q-item>-->

      </q-list>

    </q-drawer>
  <!-- this is right drawer -->
   <!-- <q-drawer
      show-if-above
      v-model="rightDrawerOpen"
      side="right"
      bordered>
      for search field
       <q-input
          color="primary"
          outlined
          rounded
          danse
          label="Search"
          class="q-ma-md"
          >
          <template v-slot:prepend>
            <q-icon name="search" />
          </template>
        </q-input>

         <q-list separator>
            <q-item >
              <q-item-section>

                <q-item-label class="text-grey" overline>Education</q-item-label>
                 <q-item-label class="text-black text-weight-bold" >Something amazing happend</q-item-label>
                <q-item-label caption lines="2">Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit.</q-item-label>
              </q-item-section>

              <q-item-section side top>
                <q-item-label caption>5 min ago</q-item-label>
                <q-icon name="star" color="yellow" />
              </q-item-section>
            </q-item>
                        <q-item >
              <q-item-section>

                <q-item-label class="text-grey" overline>Education</q-item-label>
                 <q-item-label class="text-black text-weight-bold" >Something amazing happend</q-item-label>
                <q-item-label caption lines="2">Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit.</q-item-label>
              </q-item-section>

              <q-item-section side top>
                <q-item-label caption>5 min ago</q-item-label>
                <q-icon name="star" color="yellow" />
              </q-item-section>
            </q-item>

      </q-list>

    </q-drawer> -->

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },

      rightDrawerOpen,
      toggleRightDrawer () {
        rightDrawerOpen.value = !rightDrawerOpen.value
      }
    }
  }
}
</script>
