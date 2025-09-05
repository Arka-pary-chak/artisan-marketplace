<template>
  <v-container class="d-flex flex-column align-center justify-center fill-height bg-black">
    <div class="text-h4 text-center mb-8 text-white">Who are you?</div>

    <v-row justify="center" class="pa-0 ma-0">
      <v-col cols="12" md="6" class="d-flex flex-column align-center pa-2">
        <router-link to="/artisan-profile" class="text-decoration-none">
          <v-avatar size="120" color="blue-grey-lighten-2" class="mb-2 avatar-border">
            <v-icon size="80" color="white">mdi-hammer-wrench</v-icon>
          </v-avatar>
          <div class="text-subtitle-1 text-center text-white">Artisan</div>
        </router-link>
      </v-col>

      <v-col cols="12" md="6" class="d-flex flex-column align-center pa-2">
        <router-link to="/customer-profile" class="text-decoration-none">
          <v-avatar size="120" color="orange-lighten-2" class="mb-2 avatar-border">
            <v-icon size="80" color="white">mdi-account-group</v-icon>
          </v-avatar>
          <div class="text-subtitle-1 text-center text-white">Customer</div>
        </router-link>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { VContainer, VCol,VRow , VAvatar, VIcon } from 'vuetify/components';
import { RouterLink } from 'vue-router';
</script>

<style scoped>
.bg-black {
  background-color: #000;
}

.avatar-border {
  border: 4px solid transparent;
  transition: border-color 0.3s ease;
}

.avatar-border:hover {
  border-color: #007bff;
}

.text-decoration-none {
  text-decoration: none;
}
</style>