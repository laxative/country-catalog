<template lang="pug">
.country-list-table
  .table__header
    span.table__cell__1
    span.table__cell__2 國家名稱
    span.table__cell__2 國家代碼(2位)
    span.table__cell__2 國家代碼(3位)
    span.table__cell__2 母語名稱
    span.table__cell__2 替代國家名稱
    span.table__cell__1 國際電話區號
  .table__content
    .table__content__row(v-for="(countryData, idx) in tableData" :key="idx")
      span.table__cell__1
        img.svg__flag(:src="countryData.flag")
      span.table__cell__2 {{ countryData.name }}
      span.table__cell__2 {{ countryData.alpha2Code }}
      span.table__cell__2 {{ countryData.alpha3Code }}
      span.table__cell__2 {{ countryData.nativeName }}
      .table__cell__2.alt-spelling__wrapper
        span(v-for="(altSpelling, spellingIdx) in countryData.altSpellings" :key="spellingIdx") {{ altSpelling }}
      .table__cell__1.calling-codes__wrapper
        span(v-for="(callingCode, codeIdx) in countryData.callingCodes" :key="codeIdx") {{ callingCode }}
</template>

<script lang='ts'>
import CountryRespInterface from '@/interface/CountryRespInterface';
import { Component, Prop, Vue, Watch } from 'vue-property-decorator';

@Component({
  name: 'countryListTable'
})
export default class CountryListTable extends Vue {
  @Prop({}) private tableData!: CountryRespInterface[] | undefined;
}
</script>

<style lang="scss">
@mixin table__cell($ratio) {
  width: calc(100% / 12 * #{$ratio});
}

.table__cell__1 { @include table__cell(1) }
.table__cell__2 { @include table__cell(2) }
.table__cell__3 { @include table__cell(3) }
.table__cell__4 { @include table__cell(4) }
.table__cell__5 { @include table__cell(5) }
.table__cell__6 { @include table__cell(6) }
.table__cell__7 { @include table__cell(7) }
.table__cell__8 { @include table__cell(8) }
.table__cell__9 { @include table__cell(9) }
.table__cell__10 { @include table__cell(10) }
.table__cell__11 { @include table__cell(11) }
.table__cell__12 { @include table__cell(12) }

.country-list-table {
  width: 100%;
  height: 100%;
}

.table {
  &__header {
    width: 100%;
    min-height: 40px;
    padding: 5px;

    display: flex;
    justify-content: space-evenly;
    align-items: center;

    background-color: steelblue;
    color: white;
    font-weight: bold;
  }

  &__content {
    background-color: #efefef;
    &__row {
      width: 100%;
      min-height: 60px;
      display: flex;
      // justify-content: space-evenly;
      align-items: center;
      
      padding: 5px;
      border-bottom: 1px solid #666;
    }
  }
}

.svg__flag {
  width: 80%;
  height: auto;
}

.alt-spelling__wrapper, .calling-codes__wrapper {
  display: flex;
  flex-direction: column;
}

</style>