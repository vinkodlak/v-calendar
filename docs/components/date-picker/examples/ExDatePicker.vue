<template>
  <v-date-picker
    class='picker'
    :from-page.sync='fromPage'
    :to-page.sync='toPage'
    :min-page='minPage'
    :mode='mode'
    :tint-color='tintColor'
    :show-caps='showCaps'
    :show-popover='showPopover'
    :disabled-dates='showDisabledDates ? disabledDates : null'
    :attributes='attrs'
    :is-inline='isInline'
    :is-expanded='isExpanded'
    :is-double-paned='isDoublePaned'
    :input-props='inputProps'
    :popover-expanded='popoverExpanded'
    :popover-visibility='popoverVisibility'
    :popover-direction='popoverDirection'
    :popover-align='popoverAlign'
    v-model='selectedValue'>
  </v-date-picker>
</template>

<script>
import { getExampleMonthComps } from '@/utils/helpers';
const { thisMonth, thisMonthYear, nextMonth, nextMonthYear } = getExampleMonthComps();

export default {
  props: {
    mode: { type: String, default: 'range' },
    tintColor: { type: String, default: '#66b3cc' },
    showCaps: { type: Boolean, default: true },
    showPopover: { type: Boolean, default: true },
    showDisabledDates: Boolean,
    isInline: Boolean,
    isExpanded: Boolean,
    isDoublePaned: { type: Boolean, default: true },
    popoverExpanded: Boolean,
    popoverVisibility: { type: String, default: 'visible' },
    popoverDirection: { type: String, default: 'bottom' },
    popoverAlign: { type: String, default: 'left' },
  },
  data() {
    return {
      dragValue: null,
      fromPage: null,
      toPage: null,
      minPage: { month: thisMonth+1, year: thisMonthYear },
      selectedValue: null,
      disabledDates: [
        { start: "04/08/2018", end: "04/13/2018" }
      ],
      attrs: [
        {
          key: 'today',
          bar: {
            backgroundColor: '#060606'
          },
          dates: new Date()
        },
        {
          key: 'sat',
          highlight: {
            backgroundColor: '#2baaff'
          },
          contentStyle: {
            color: '#fff'
          },
          contentHoverStyle: {
            // cursor: 'pointer'
          },
          dates: { start: new Date(), end: null, weekdays: [7] }
        },
        {
          key: 'notAllowed',
          contentStyle: {
            color: '#ccc'
          },
          contentHoverStyle: {
            cursor: 'not-allowed',
            backgroundColor: 'transparent'
          },
          dates: { weekdays: [1,2,3,4,5,6] }
        },
        {
          key: 'notAllowedSat',
          contentStyle: {
            color: '#ccc'
          },
          contentHoverStyle: {
            cursor: 'not-allowed',
            backgroundColor: 'transparent'
          },
          dates: { start: null, end: new Date()-86400000, weekdays: [7] }
        }
      ],
      inputProps: {
        class: 'input',
      },
    };
  },
};
</script>

<style lang='sass'>
.picker
  min-width: 220px
</style>
