<template>
  <v-container class="d-flex align-center justify-center fill-height bg-black">
    <v-card class="mx-auto" max-width="500" theme="dark">
      <v-card-title class="text-h5">
        Customer Profile Creation
      </v-card-title>
      <v-card-text>
        <v-form @submit.prevent="handleSubmit">
          <v-text-field
            label="Your Name"
            required
            v-model="formData.name"
          ></v-text-field>
          <v-text-field
            label="Your Location"
            required
            v-model="formData.location"
          ></v-text-field>

          <h4 class="mt-4">Preferred Language (Select up to 2)</h4>
          <v-chip-group multiple max="2" v-model="formData.language">
            <v-chip
              v-for="language in languages"
              :key="language"
              filter
              variant="outlined"
              size="large"
              selected-class="bg-blue"
            >
              {{ language }}
            </v-chip>
          </v-chip-group>

          <h4 class="mt-4">ID Card Information</h4>
          <v-select
            label="ID Card Type"
            :items="idTypes"
            v-model="formData.idType"
          ></v-select>

          <v-text-field
            v-if="formData.idType"
            label="ID Number"
            v-model="formData.idNumber"
            type="text"
          ></v-text-field>
          <v-file-input
            v-if="formData.idType"
            label="Upload ID Card Image"
            v-model="formData.idCardImage"
            prepend-icon="mdi-camera"
            chips
          ></v-file-input>

          <h4 class="mt-4">Products you are interested in(One or More)</h4>
          <v-chip-group multiple v-model="formData.product">
            <v-chip
              v-for="product in products"
              :key="product"
              filter
              variant="outlined"
              size="large"
              selected-class="bg-blue"
            >
              {{ product }}
            </v-chip>
          </v-chip-group>

          <v-btn
            type="submit"
            color="primary"
            class="mt-4"
            block
          >
            Create Profile
          </v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script setup>
import { ref } from 'vue'
import { VContainer, VCard, VCardTitle, VCardText, VTextField, VChipGroup, VChip, VBtn, VForm, VIcon, VFileInput, VSelect } from 'vuetify/components'

const languages = ['English', 'Hindi', 'Tamil', 'Bengali', 'Marathi']
const idTypes = ['Aadhar Card', 'Ration Card', 'Passport']
const products = ['Pottery', 'Art', 'Clothing', 'Jewelry']

const formData = ref({
  name: '',
  location: '',
  language: [],
  idType: null,
  idNumber: null,
  idCardImage: null,
  product: []
})


const handleSubmit = () => {
  console.log('Customer form data:', formData.value)
}
</script>

<style scoped>
.bg-black {
  background-color: #000;
}
</style>