<template>
  <v-card>
    <v-card-title>
      <span class="headline">{{ formTitle }}</span>
    </v-card-title>
    <v-card-text>
      <v-form
        ref="form"
        v-model="valid"
        lazy-validation
      >
        <v-container>
          <v-row>
            <v-col
              cols="12"
              sm="6"
              md="6"
            >
              <v-text-field
                v-model="editedItem.name"
                label="Company Name"
                :rules="nameRules"
              ></v-text-field>
            </v-col>
            <v-col
              cols="12"
              sm="6"
              md="6"
            >
              <v-text-field
                v-model="editedItem.address"
                label="Company Address"
                :rules="addressRules"
              ></v-text-field>
            </v-col>
            <v-col
              cols="12"
              sm="6"
              md="6"
            >
              <v-text-field
                v-model="editedItem.country"
                label="Country"
                :rules="countryRules"
              ></v-text-field>
            </v-col>
            <v-col
              cols="12"
              sm="6"
              md="6"
            >
              <v-text-field
                v-model="editedItem.city"
                label="City"
                :rules="cityRules"
              ></v-text-field>
            </v-col>
            <v-col
              cols="12"
              sm="6"
              md="6"
            >
              <v-text-field
                v-model="editedItem.email"
                label="Email Address"
                :rules="emailRules"
              ></v-text-field>
            </v-col>
            <v-col
              cols="12"
              sm="12"
              md="12"
            >
              <v-textarea
                filled
                label="Description"
                auto-grow
                v-model="editedItem.description"
                :rules="descriptionRules"
              ></v-textarea>
            </v-col>
          </v-row>
        </v-container>
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        color="blue darken-1"
        text
        @click="$emit('close')"
        v-if="editing"
      >
        Cancel
      </v-btn>
      <v-btn
        color="blue darken-1"
        text
        @click="validate"
      >
        Save
      </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
  export default {
    name: 'company-form',
    props: {
      editedItem: {},
      formTitle: '',
      editing: false
    },
    data() {
      return {
        editItem: this.editedItem,
        nameRules: [
          v => !!v || 'Name is required'
        ],
        addressRules: [
          v => !!v || 'Address is required'
        ],
        cityRules: [
          v => !!v || 'City is required'
        ],
        countryRules: [
          v => !!v || 'Country is required',
        ],
        emailRules: [
          v => !!v || 'Email is required',
          v => /.+@.+\..+/.test(v) || 'Email must be valid',
        ],
        descriptionRules: [
          v => !!v || 'Description is required',
          v => (v && v.length >= 10) || 'Name must be at least 10 characters',
        ],
        valid: true,
      }
    },
    methods: {
      validate() {
        this.$refs.form.validate();
        if (this.valid && this.$refs.form.validate()) {
          this.$emit('save-item')
        }
      },
    }
  }
</script>
