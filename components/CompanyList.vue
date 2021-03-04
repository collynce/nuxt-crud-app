<template>
  <div>
    <div v-if="companies.length>0">
      <template>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="50%"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              Add Company
            </v-btn>
          </template>
          <company-form
            @save-item='save'
            :formTitle="formTitle"
            :editing="true"
            @close="close"
            :editedItem="editedItem"
          />
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="headline">Are you sure you want to delete this item?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </template>
      <company-cards
        :companies="companies"
        @delete-item="deleteItem($event)"
        @edit-item="editItem($event)"
        :loading="loading"/>
    </div>
    <div v-else>
      <company-form
        @save-item='save'
        :formTitle="formTitle"
        :editing="editing"
        :editedItem="editedItem"
        @close="close"
      />
    </div>
  </div>
</template>
<script>
  import CompanyForm from "./CompanyForm.vue";
  import CompanyCards from "./CompanyCards";

  export default {
    components: {CompanyCards, CompanyForm},
    data: () => ({
      loading: false,
      selection: 1,
      dialog: false,
      dialogDelete: false,
      companies: [],
      editedIndex: -1,
      editedItem: {},
      defaultItem: {},
      editing: false
    }),

    computed: {
      formTitle() {
        return this.editedIndex === -1 ? 'New Company' : 'Edit Company'
      }
    },

    watch: {
      dialog(val) {
        val || this.close()
      },
      dialogDelete(val) {
        val || this.closeDelete()
      },
    },

    created() {
      this.initialize()
    },

    methods: {
      initialize() {
        this.companies = [
          {
            "name": "Paulita",
            "city": "Valletta",
            "country": "Kyrgyzstan",
            "email": "Paulita@yopmail.com",
            "description": "helloooooooooooooooooooooooo world",
            "address": "Valletta, Kyrgyzstan"
          },
          {
            "name": "Corina",
            "city": "Cleveland",
            "country": "RWANDA",
            "email": "Corina@yopmail.com",
            "description": "helloooooooooooooooo to you",
            "address": "Cleveland, RWANDA"
          },
          {
            "name": "Margarette",
            "city": "Cartagena",
            "country": "Latvia",
            "email": "Margarette@yopmail.com",
            "description": "helloooooo to you",
            "address": "Cartagena, Latvia"
          }
        ]
      },
      editItem(item) {
        this.editing = true;
        this.editedIndex = this.companies.indexOf(item);
        this.editedItem = Object.assign({}, item);
        this.dialog = true
      },

      deleteItem(item) {
        this.editedIndex = this.companies.indexOf(item);
        this.editedItem = Object.assign({}, item);
        this.dialogDelete = true
      },

      deleteItemConfirm() {
        this.companies.splice(this.editedIndex, 1);
        this.closeDelete()
      },

      close() {
        this.dialog = false;
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem);
          this.editedIndex = -1
        })
      },

      closeDelete() {
        this.dialogDelete = false;
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem);
          this.editedIndex = -1
        })
      },

      save() {
        if (this.editedIndex > -1) {
          Object.assign(this.companies[this.editedIndex], this.editedItem)
        } else {
          this.companies.push(this.editedItem)
        }
        this.close()
      },
    },
  }
</script>
