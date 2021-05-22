<template lang="pug">
.model
  .model__row(v-for="(title, keyIdx) in dataKeys")
    .model__title.table__cell__3 {{ title }}
    .model__content.table__cell__9 {{ countryData[title] }}
  .model__close__button(@click="onClickEvent") 關閉
</template>

<script lang='ts'>
import CountryRespInterface from '@/interface/CountryRespInterface';
import { Component, Prop, Vue, Watch, Emit } from 'vue-property-decorator';

@Component({
  name: 'countryDataModel'
})
export default class CountryListTable extends Vue {
  @Prop({}) private countryData!: CountryRespInterface | undefined;

  private dataKeys: string[] = [];

  @Watch('countryData')
  onCountryDataChanged() {
    if (this.countryData) {
      this.dataKeys = Object.keys(this.countryData);
      // console.log(this.dataKeys)
      this.$el.scrollTo(0, 0)
    } else {
      this.dataKeys = [];
    }
  }

  @Emit('submit-close-detail-event')
  onClickEvent() {}
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

.model {
  position: fixed;
  top: 0;
  left: 0;
  padding: 5%;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, .75);
  word-break: break-all;

  overflow-y: scroll;
  overflow-x: none;

  &__row {
    width: 100%;
    display: flex;
    align-items: stretch;
    margin-bottom: 1px;
  }

  &__title, &__content {
    min-height: 30px;
    display: flex;
    align-items: center;
  }

  &__title {
    background-color: rgb(38, 134, 70);
    color: white;
    justify-content: center;
    padding: 3px;
  }

  &__content {
    background-color: #efefef;
    justify-content: flex-start;
    text-align: left;
    padding: 10px 20px;
  }
}

.model__close__button {
  margin-top: 20px;
  padding: 10px;
  color: #fff;
  border: 1px solid #fff;
  opacity: .5;
  cursor: pointer;

  transition: all .3s ease;

  &:hover {
    opacity: 1;
  }
}
</style>