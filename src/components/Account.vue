<template>
  <v-layout>
      <v-navigation-drawer
        id="navigation"
        permanent
        touchless
        dark
        width="180"
        :height="600"
        fill-height
        :mini-variant.sync="iconsOnly"
      >
        <v-list>
          <v-list-tile
            @click="$router.push('profile')"
          >
            <v-list-tile-action>
              <v-icon>account_circle</v-icon>
            </v-list-tile-action>
            <v-list-tile-title>Profile</v-list-tile-title>
          </v-list-tile>
          <v-list-group
            prepend-icon="vpn_key"
            value="true"
          >
            <v-list-tile slot="activator">
              <v-list-tile-title>Security</v-list-tile-title>
            </v-list-tile>
            <v-list-tile
              @click="$router.push('signin')"
            >
              <v-list-tile-title>Sign in</v-list-tile-title>
              <v-list-tile-action>
                <v-icon>security</v-icon>
              </v-list-tile-action>
            </v-list-tile>
            <v-list-tile
              @click="$router.push('twofactor')"
            >
              <v-list-tile-title>2-Factor</v-list-tile-title>
              <v-list-tile-action>
                <v-icon>fingerprint</v-icon>
              </v-list-tile-action>
            </v-list-tile>
            <v-list-tile
              @click="$router.push('audit')"
            >
              <v-list-tile-title>Audit</v-list-tile-title>
              <v-list-tile-action>
                <v-icon>find_in_page</v-icon>
              </v-list-tile-action>
            </v-list-tile>

          </v-list-group>
          <v-list-tile
            @click="$router.push('data')"
          >
            <v-list-tile-action>
              <v-icon>assessment</v-icon>
            </v-list-tile-action>
            <v-list-tile-title>Data</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-navigation-drawer>

    <v-container id="content">
      <second-factor v-if="screen == 'twofactor'">
      </second-factor>
      <profile v-if="screen == 'profile'"></profile>
      <primary-factor v-if="screen == 'signin'"></primary-factor>
      <audit v-if="screen == 'audit'"></audit>
      <data-view v-if="screen == 'data'"></data-view>
    </v-container>
  </v-layout>
</template>

<script>
    import SecondFactor from '@/components/secondfactor/SecondFactor'
    import PrimaryFactor from '@/components/PrimaryFactor'
    import Profile from '@/components/Profile'
    import Audit from '@/components/Audit'
    import DataView from '@/components/DataView'

    export default {
      name: 'Account',
      data () {
        return {
          drawer: true
        }
      },
      components: {
        SecondFactor,
        PrimaryFactor,
        Profile,
        Audit,
        DataView
      },
      created: function () {
        this.$vuetify.theme.titlebar = this.$vuetify.theme.primary
      },
      computed: {
        screen: {
          get: function () {
            return this.$route.params.page
          }
        },
        iconsOnly: {
          get: function () {
            switch (this.$vuetify.breakpoint.name) {
              case 'xs':
                return true
              case 'sm':
                return false
              case 'md':
                return false
              case 'lg':
                return false
              case 'xl':
                return false
            }
          },
          set: () => {}
        }
      }
    }
</script>

<style scoped>
  #navigation {
    display: inline-block;
  }

  #content {
    display: inline-block;
  }
</style>
