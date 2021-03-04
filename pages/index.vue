<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="12" md="12">
      <company-list></company-list>
    </v-col>
  </v-row>
</template>

<script>
import CompanyList from "../components/CompanyList";

export default {
  components: {
    CompanyList
  }
}
</script>
