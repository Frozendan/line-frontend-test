<template>
    <v-app>
        <nav-bar></nav-bar>
        <v-content class="main-content">
            <v-container class="pt-0" fluid>
                <!--I do not create router here because we are working on a single screen only (for simplicity of the test)
                    So I import the component directly in the main page-->
                <TimelinePost></TimelinePost>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
import NavBar from "@/components/NavBar";
import TimelinePost from "@/components/TimelinePost";

export default {
  name: 'App',

  components: {
      NavBar,
      TimelinePost
  },

  data: () => ({
    //
  }),
};
</script>
<style lang="scss">
    @import 'assets/scss/main.scss';
    /*For the same reason as above, I write style directly in the component for modification*/
    /*and use the default style of vuetify*/
  body {
    font-family: Avenir, Helvetica, Arial, sans-serif;
  }
    .main-content {
        margin-top: 128px;
    }
</style>