<template lang="pug">
.catalog__container
</template>

<script lang="ts">
interface countryRespInterface {
  name: string,
  topLevelDomain: string[],
  alpha2Code: string,
  alpha3Code: string,
  callingCodes: string[],
  capital: string,
  altSpellings: string[],
  region: string,
  subregion: string,
  population: number,
  latlng: number[],
  demonym: string,
  area: number,
  gini: number,
  timezones: string[],
  borders: string[],
  nativeName: string,
  numericCode: string,
  currencies: {
    code: string,
    name: string,
    symbol: string
  }[],
  languages: {
    iso639_1: string,
    iso639_2: string,
    name: string,
    nativeName: string
  }[],
  translations: {
    [name: string]: string
  },
  flag: string,
  regionalBlocs: {
    acronym: string,
    name: string,
    otherAcronyms: string[],
    otherName: string[]
  }[],
  cioc: string
}



import { Component, Prop, Vue, Watch } from 'vue-property-decorator';
@Component
export default class Catalog extends Vue {
  private countriesAPIResp !:countryRespInterface[];

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