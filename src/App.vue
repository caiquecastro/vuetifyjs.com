<template>
  <v-fade-transition appear>
    <documentation v-if="!examples" />
    <div
      v-else
      id="app"
    >
      <router-view />
    </div>
  </v-fade-transition>
</template>

<script>
  import Documentation from '@/components/core/Documentation'
  import Meta from '@/mixins/meta'

  import {
    mapMutations,
    mapState
  } from 'vuex'

  export default {
    components: {
      Documentation
    },

    mixins: [Meta],

    computed: {
      ...mapState({
        isFullscreen: state => state.isFullscreen
      }),
      examples () {
        return !!this.$route.params.example
      }
    },

    mounted () {
      this.getReleases()

      this.snackbar({
        color: 'default',
        close: true,
        id: 'may-2018-update-19449773',
        text: 'Go To Update',
        msg: '**New Patreon Update** — _May 2018 Update_',
        href: 'https://www.patreon.com/posts/may-2018-update-19449773',
        timeout: 0
      })
    },

    methods: {
      ...mapMutations('app', {
        snackbar: 'SNACKBAR'
      }),
      getReleases () {
        this.$http.get('/releases/releases.json').then(({ data }) => {
          this.$store.commit('app/RELEASES', data)
        }).catch(err => {
          console.log(err)
        })
      }
    }
  }
</script>

<style lang="stylus">
  @import '~vuetify/src/stylus/settings/_variables.styl'

  main
    section
      &:before
        content ''
        display block
        position relative
        width 0
        height 80px
        margin-top -80px

  .container.page
    max-width: 1185px !important
    padding-top: 75px
    padding-bottom: 0
    transition: .2s $transition.fast-out-slow-in

    section
      margin-bottom: 48px
</style>
