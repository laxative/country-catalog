<template lang="pug">
.catalog__container
  CountryListTable(:tableData="countriesAPIResp" v-if="countriesAPIResp.length")
</template>

<script lang="ts">
import CountryRespInterface from '@/interface/CountryRespInterface';
import { Component, Prop, Vue, Watch } from 'vue-property-decorator';

import CountryListTable from '@/components/CountryListTable.vue';

@Component({
  components: {
    CountryListTable
  }
})

export default class Catalog extends Vue {
  private countriesAPIResp: CountryRespInterface[] = [];

  public created() {
    // get country list via API
    fetch('https://restcountries.eu/rest/v2/all').then((response) => {
      return response.json()
    }).then((jsonResp) => {
      this.countriesAPIResp = jsonResp;
      console.log(this.countriesAPIResp)
    }) 
  }
}

</script>

<style lang="scss">
.catalog__container {
  width: 100%;
  height: 100%;
  padding: 25px;
}
</style>