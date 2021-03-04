<template>
  <v-container>
    <v-row>
      <v-col v-for="(company,index) in companies" cols="4" :key="index">
        <v-card
          :loading="loading"
          class="mx-auto my-12"
        >
          <template slot="progress">
            <v-progress-linear
              color="deep-purple"
              height="10"
              indeterminate
            ></v-progress-linear>
          </template>

          <v-img
            :src="`https://picsum.photos/250/300?image=${index * 5 + 10}`"
            :lazy-src="`https://picsum.photos/10/6?image=${index * 5 + 10}`"
            aspect-ratio="1"
            height="250"
            class="grey lighten-2"
          >
            <template v-slot:placeholder>
              <v-row
                class="fill-height ma-0"
                align="center"
                justify="center"
              >
                <v-progress-circular
                  indeterminate
                  color="grey lighten-5"
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>

          <v-card-title>
            <p>Name: {{company.name}}</p>
          </v-card-title>

          <v-card-text>
            <v-row
              align="start"
              class="mx-0"
            >
              <div class="grey--text">
                <p>Email: {{company.email}}</p>
              </div>
            </v-row>
            <div class="mb-4 subtitle-1">
              <p>Location: {{company.country + ', ' + company.city}}</p>
            </div>
            <div>
              <span><strong>Description</strong></span>
              <p>{{company.description}}</p>
            </div>
          </v-card-text>

          <v-divider class="mx-4"></v-divider>
          <v-row justify="end">
            <v-col cols="12" sm="12" md="12">
              <v-card-actions>
                <v-icon
                  small
                  class="mr-2"
                  @click="$emit('edit-item',company)"
                >
                  mdi-pencil
                </v-icon>
                <v-icon
                  small
                  @click="$emit('delete-item', company)"
                >
                  mdi-delete
                </v-icon>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
  export default {
    name: 'company-cards',
    props: {
      companies: {},
      loading: {}
    }
  }
</script>
