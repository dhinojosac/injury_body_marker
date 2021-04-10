<template>
  <v-app>
    <v-main>
       <human-plan/>
    </v-main>
  </v-app>
</template>

<script>
import HumanPlan from "./components/HumanPlan.vue"

export default {
  name: 'App',

  components: {
    HumanPlan,
  },

  data: () => ({
    //
  }),
};
</script>
