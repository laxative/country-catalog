<template lang="pug">
.catalog__container
  .function__bar
    .sorting__switch__wrapper
      span 正序
      label.switch
        input(type="checkbox" v-model="isDesc")
        span.slider.round
      span 倒序
    .searching__input__wrapper
      input.searching__input(v-model="searchingKeyWords" placeholder="請輸入欲搜尋的國家名稱")
  CountryListTable(:tableData="showingData" v-if="countriesAPIResp.length")
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
  private showingData: CountryRespInterface[] = [];

  private isDesc: boolean = false;
  private searchingKeyWords: string = '';

  @Watch('searchingKeyWords')
  onSearchingKeyWordsChanged(value: string, oldValue: string) {
    this.filterData(value);
    this.sortData(this.isDesc);
  }

  @Watch('isDesc')
  onIsDescChanged(value: boolean, oldValue: boolean) {
    this.sortData(value);
  }

  public created() {
    // get country list via API
    fetch('https://restcountries.eu/rest/v2/all').then((response) => {
      return response.json()
    }).then((jsonResp) => {
      this.countriesAPIResp = jsonResp;
      this.showingData = JSON.parse(JSON.stringify(this.countriesAPIResp));
      this.sortData(this.isDesc);
    }) 
  }

  private filterData(countryName: string) {
    this.showingData = this.countriesAPIResp.filter((countryData) => {
      return countryData.name.includes(countryName)
    })
  }

  private sortData(isDesc: boolean) {
    this.showingData = this.showingData.sort((a, b) => {
      if (isDesc) {
        return a.name < b.name ? 1 : -1
      } else {
        return a.name > b.name ? 1 : -1
      }
    })
  }
}

</script>

<style lang="scss">
.catalog__container {
  width: 100%;
  height: 100%;
  padding: 25px;

  .function__bar {
    width: 100%;
    margin-bottom: 20px;
    display: flex;
    justify-content: flex-end;
    flex-wrap: wrap;
    align-items: center;

    > * {
      margin: 5px 10px;
    }

    .sorting__switch__wrapper {
      display: flex;
      align-items: center;

      > * {
        margin: 0 5px;
      }

      span {
        color: #666;
        font-weight: bold;
      }

      // switch button style below
      .switch {
        position: relative;
        display: inline-block;
        width: 60px;
        min-width: 60px;
        height: 34px;
      }

      .switch input {
        opacity: 0;
        width: 0;
        height: 0;
      }

      .slider {
        position: absolute;
        cursor: pointer;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: #ccc;
        transition: .4s;
      }

      .slider:before {
        position: absolute;
        content: "";
        height: 26px;
        width: 26px;
        left: 4px;
        bottom: 4px;
        background-color: #fff;
        transition: .4s;
      }

      input:checked + .slider {
        background-color: #2196F3;
      }

      input:focus + .slider {
        box-shadow: 0 0 1px #2196F3;
      }

      input:checked + .slider:before {
        transform: translateX(26px);
      }

      .slider.round {
        border-radius: 34px;
      }

      .slider.round:before {
        border-radius: 50%;
      }
    }

    .searching__input__wrapper {
      .searching__input {
        padding: 0 10px;
        height: 34px;
        line-height: 34px;
        font-size: 16px;
        font-weight: bold;
        color: #666;
        width: 250px;
        min-width: 250px;

        &::placeholder {
          color: #bbb;
          font-size: 14px;
        }
      }
    }
  }
}
</style>