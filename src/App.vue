<template>
  <v-app>
    <v-main>
      <Activity/>
    </v-main>
  </v-app>
</template>

<script>
import Activity from './components/Activity';

export default {
  name: 'App',

  components: {
    Activity,
  },

  data: () => ({
    //
  }),
};
</script>
