<template lang="pug">
  doc-view
    template(slot-scope="{ namespace }")
      section#playground
        section-head(:value="`${namespace}.playgroundHeader`")
        section-text(:value="`${namespace}.playgroundText`")
        spacing-playground

      section#how-it-works
        section-head(value="Generic.Pages.howItWorks")
        section-text(:value="`${namespace}.howText`")
        section-text(:value="`${namespace}.propertyText`")
        ul.browser-list.pb-2
          li(
            v-for="item in properties"
            :key="item"
          )
            markdown(:source="item")
        section-text(:value="`${namespace}.directionText`")
        ul.browser-list.pb-2
          li(
            v-for="item in directions"
            :key="item"
          )
            markdown(:source="item")
        section-text(:value="`${namespace}.sizeText`")
        ul.browser-list
          li(
            v-for="item in sizes"
            :key="item"
          )
            markdown(:source="item")
</template>

<script>
  export default {
    computed: {
      directions () {
        return this.$t('Layout.Spacing.directions')
      },
      properties () {
        return this.$t('Layout.Spacing.properties')
      },
      sizes () {
        return this.$t('Layout.Spacing.sizes')
      }
    }
  }
</script>
