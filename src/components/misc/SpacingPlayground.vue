<template lang="pug">
  v-container(class="spacing-playground" grid-list-lg)
    v-layout(row wrap)
      v-flex(xs12 sm6 class="d-flex align-center")
        v-select(:items="directions" label="Direction" class="pr-2" v-model="paddingDirection")
          div(slot="prepend") p
          div(slot="append-outer") -
        v-select(:items="sizes" label="Size" v-model="paddingSize")
      v-flex(xs12 sm6 class="d-flex")
        v-select(:items="directions" label="Direction" class="px-2" v-model="marginDirection")
          div(slot="prepend") m
          div(slot="append-outer") -
        v-select(:items="sizes" label="Size" v-model="marginSize")
      v-flex(xs12 class="orange lighten-3 pa-0")
        v-card(:class="[computedMargin]" class="elevation-4")
          div(:class="[computedPadding]" class="light-green lighten-3")
            div(class="white text-xs-center") Use the controls above to try out the different spacing helpers
</template>

<script>
  export default {
    data: () => ({
      directions: ['t', 'b', 'l', 'r', 'x', 'y', 'a'],
      sizes: ['0', '1', '2', '3', '4', '5'],
      paddingDirection: 'a',
      paddingSize: '2',
      marginDirection: 'a',
      marginSize: '2'
    }),
    computed: {
      computedPadding () {
        return `p${this.paddingDirection}-${this.paddingSize}`
      },
      computedMargin () {
        return `m${this.marginDirection}-${this.marginSize}`
      }
    }
  }
</script>

<style>
  .spacing-playground .v-select .v-input__prepend-outer, .spacing-playground .v-select .v-input__append-outer{
    margin-top: 0.55rem;
    margin-right: 0.2rem;
  }
</style>
