
<template>
  <div id="n1" />
  <router-view />
  <v-card max-width="448" class="mx-auto" color="grey-lighten-3">
    <v-layout>

      <v-app-bar :elevation="7" color="teal-darken-4" image="https://drramiro.com.br/wp-content/uploads/2018/03/Liquido.jpg">
        <template v-slot:image>
          <v-img gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"></v-img>
        </template>

        

        <v-tab>
          <!--  -->
          <v-btn class="mx-4 white--text" elevation="4" color="e8eaf6 indigo lighten-5" to="/">
            Home
          </v-btn>

        </v-tab>

        <v-tab>
          <v-btn class="mx-4 white--text" elevation="2" x-large color="e8eaf6 indigo lighten-5" to="/cadastro">
            Cadastro
          </v-btn>

        </v-tab>

        

        <!--  -->

      </v-app-bar>
    </v-layout>
  </v-card>
</template>

<script>


</script>
<style>
#n1 {
  margin: 10px 0 0 0;
}
</style>

