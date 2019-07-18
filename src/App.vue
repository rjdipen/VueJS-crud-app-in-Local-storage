<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Crud</span>
        <span class="font-weight-light">App</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        flat

      >
        <span class="mr-2">Local storage</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <task/>
    </v-content>
  </v-app>
</template>

<script>
import Task from "./components/Task";

export default {
  name: 'App',
  components: {
      Task,
  },
  data () {
    return {
      //
    }
  }
}
</script>
