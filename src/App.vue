<template>
  <v-app>
    <v-main>
      <NetWork/>
    </v-main>
  </v-app>
</template>

<script>
import NetWork from './components/NetWork';

export default {
  name: 'App',

  components: {
    NetWork,
  },

  data: () => ({
    //
  }),
};
</script>
