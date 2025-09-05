<template>
  <v-container class="d-flex align-center justify-center fill-height bg-black">
    <v-card class="mx-auto" max-width="500" theme="dark">
      <v-card-title class="text-h5">
        Profile Creation
      </v-card-title>
      <v-card-text>
        <v-form ref="form" @submit.prevent="handleSubmit">
          <v-text-field
            label="Artisan Name"
            required
            v-model="formData.name"
            :rules="[rules.required]"
          >
            <template v-slot:append-inner>
              <v-icon color="primary" @click="handleVoiceInput('name')">mdi-microphone</v-icon>
            </template>
          </v-text-field>
          <v-text-field
            label="Artisan's Location"
            required
            v-model="formData.location"
            :rules="[rules.required]"
          >
            <template v-slot:append-inner>
              <v-icon color="primary" @click="handleVoiceInput('location')">mdi-microphone</v-icon>
            </template>
          </v-text-field>

          <v-select
            label="ID Card Type"
            :items="idTypes"
            v-model="formData.idType"
            :rules="[rules.required]"
          ></v-select>

          <v-text-field
            v-if="formData.idType"
            label="ID Number"
            v-model="formData.idNumber"
            type="text"
            :rules="[rules.required]"
          ></v-text-field>
          <v-file-input
            v-if="formData.idType"
            label="Upload ID Card Image"
            v-model="formData.idCardImage"
            prepend-icon="mdi-camera"
            chips
            :rules="[rules.required]"
          ></v-file-input>

          <h4 class="mt-4">Preferred Instruction Language (Select one)</h4>
          <v-chip-group mandatory v-model="formData.instructionLanguage" :rules="[rules.chipRequired]">
            <v-chip
              v-for="language in instructionLanguages"
              :key="language"
              filter
              variant="outlined"
              size="large"
              selected-class="bg-blue"
            >
              {{ language }}
            </v-chip>
          </v-chip-group>
          
          <h4 class="mt-4">Preferred Text Languages (Select up to 2)</h4>
          <v-chip-group multiple :max="2" v-model="formData.language" :rules="[rules.chipRequired]">
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

          <h4 class="mt-4">Products (Select one or more)</h4>
          <v-chip-group multiple v-model="formData.product" :rules="[rules.chipRequired]">
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

const form = ref(null)

const languages = ['English', 'Hindi', 'Tamil', 'Bengali', 'Marathi']
const instructionLanguages = ['English', 'Hindi', 'Tamil']
const products = ['Pottery', 'Art', 'Clothing', 'Jewelry']
const idTypes = ['Aadhar Card', 'Ration Card', 'Passport']

const formData = ref({
  name: '',
  location: '',
  idType: null,
  idNumber: null,
  idCardImage: null,
  language: [],
  instructionLanguage: null,
  product: []
})

const rules = {
  required: value => !!value || 'This field is required',
  chipRequired: value => value.length > 0 || 'Please select at least one option'
}

const handleSubmit = async () => {
  const { valid } = await form.value.validate()

  if (valid) {
    console.log('Form data is valid:', formData.value)
    alert('Form data is valid! Ready to send to the backend.')
  } else {
    console.log('Form data is invalid')
    alert('Please fill out all required fields.')
  }
}

const handleVoiceInput = (field) => {
  console.log(`Voice input requested for field: ${field}`)
}
</script>

<style scoped>
.bg-black {
  background-color: #000;
}
</style>