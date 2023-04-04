
<template>
  <div class="my-component">
    <v-card>
      <v-tabs color="deep-purple-accent-4" align-tabs="center">
        <v-tab>
          <router-link to="/">Home</router-link>
        </v-tab>
        <v-tab>
          <router-link to="/cadastro">Cadastro</router-link>
        </v-tab>
      </v-tabs>
    </v-card>
    <!-- injection -->
    <router-view />
  </div>
</template>



<script setup>

</script>
<style>
.my-component3{
  background: linear-gradient(270deg, #000000, #09749b);
}
</style>

