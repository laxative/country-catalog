<template lang="pug">
.country-list-table
  .table__header
    //- header title only show in laptop
    .table__content__laptop
      span.table__cell__1
      span.table__cell__2 國家名稱
      span.table__cell__2 國家代碼(2位)
      span.table__cell__2 國家代碼(3位)
      span.table__cell__2 母語名稱
      span.table__cell__2 替代國家名稱
      span.table__cell__1 國際電話區號
  .table__content
    .table__content__row(v-for="(countryData, idx) in tableData" :key="idx")
      //- laptop style
      .table__content__laptop
        span.table__cell__1
          img.svg__flag(:src="countryData.flag")
        span.table__cell__2.table__cell__click__element(@click="onCountryNameClick(idx)") {{ countryData.name }}
        span.table__cell__2 {{ countryData.alpha2Code }}
        span.table__cell__2 {{ countryData.alpha3Code }}
        span.table__cell__2 {{ countryData.nativeName }}
        .table__cell__2.alt-spelling__wrapper
          span(v-for="(altSpelling, spellingIdx) in countryData.altSpellings" :key="spellingIdx") {{ altSpelling }}
        .table__cell__1.calling-codes__wrapper
          span(v-for="(callingCode, codeIdx) in countryData.callingCodes" :key="codeIdx") {{ callingCode }}
      //- mobile style
      .table__content__mobile
        span.table__cell__2
          img.svg__flag(:src="countryData.flag")
        .table__cell__10
          .table__cell__mobile__content__wrapper
            span.table__cell__5 國家名稱
            span.table__cell__7.table__cell__click__element(@click="onCountryNameClick(idx)") {{ countryData.name }}
          .table__cell__mobile__content__wrapper
            span.table__cell__5 國家代碼(2位)
            span.table__cell__7 {{ countryData.alpha2Code }}
          .table__cell__mobile__content__wrapper
            span.table__cell__5 國家代碼(3位)
            span.table__cell__7 {{ countryData.alpha3Code }}
          .table__cell__mobile__content__wrapper
            span.table__cell__5 母語名稱
            span.table__cell__7 {{ countryData.nativeName }}
          .table__cell__mobile__content__wrapper
            span.table__cell__5 替代國家名稱
            span.table__cell__7.alt-spelling__wrapper
              span(v-for="(altSpelling, spellingIdx) in countryData.altSpellings" :key="spellingIdx") {{ altSpelling }}
          .table__cell__mobile__content__wrapper
            span.table__cell__5 國際電話區號
            span.table__cell__7.calling-codes__wrapper
              span(v-for="(callingCode, codeIdx) in countryData.callingCodes" :key="codeIdx") {{ callingCode }}
</template>

<script lang='ts'>
import CountryRespInterface from '@/interface/CountryRespInterface';
import { Component, Prop, Vue, Emit, Watch } from 'vue-property-decorator';

@Component({
  name: 'countryListTable'
})
export default class CountryListTable extends Vue {
  @Prop({}) private tableData!: CountryRespInterface[] | undefined;

  @Emit('submit-open-detail-event')
  onCountryNameClick(idx: number) {
    if (this.tableData) return this.tableData[idx];
  }
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

.table__cell__click__element {
  cursor: pointer;
  color: blue;
  text-decoration: underline;
  transition: all .2s ease;

  &:hover {
    color: red;
  }
}

.table__content__laptop, .table__cell__mobile__content__wrapper {
  display: flex;
  align-items: stretch;
  text-align: left;
}

.table__cell__mobile__content__wrapper > * {
  display: flex;
  align-items: center;
}

.table__cell__mobile__content__wrapper > *:first-child {
  padding-right: 10px;
  text-align: right;
}

.country-list-table {
  width: 100%;
}

.table {
  &__header {
    width: 100%;
    min-height: 40px;
    padding: 5px;
    text-align: left;

    display: flex;
    justify-content: space-evenly;
    align-items: stretch;

    background-color: steelblue;
    color: white;
    font-weight: bold;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
  }

  &__content {
    background-color: #efefef;
    overflow-y: auto;
    overflow-x: hidden;
    height: auto;

    &__row {
      width: 100%;
      padding: 5px;
      border-bottom: 1px solid #666;
    }

    &__laptop, &__mobile {
      width: 100%;
      min-height: 60px;
      display: flex;
      align-items: center;
    }
  }
}

@media screen and (max-width: 768px) {
  .table__content__laptop {
    display: none;
  }
}

@media screen and (min-width: 769px) {
  .table__content__mobile {
    display: none;
  }
}

.svg__flag {
  width: 80%;
  height: auto;
}

.alt-spelling__wrapper, .calling-codes__wrapper {
  display: flex;
  flex-wrap: wrap;

  > * {
    &:not(:first-child) {
      &:before {
        content: ', ';
      }
    }
  }
}

</style>