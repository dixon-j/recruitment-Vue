<template>
    <v-navigation-drawer app mini-variant expand-on-hover permanent>
      <v-list-item>
        <v-list-item-icon>
        <v-icon medium>mdi-account-multiple-check</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>
            Recruitment Vue
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="page in pages"
          :key="page.title"
          link
          :to = page.link
        >
          <v-list-item-icon>
            <v-icon>{{ page.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ page.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <template v-slot:append>
        <v-divider></v-divider>
        <v-list-item>
          <v-list-item-icon>
          <v-icon medium>mdi-account</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>
              Account
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </template>
    </v-navigation-drawer>
</template>
<script>
export default {
  data () {
    return {
      pages: [
        { title: 'Chats', icon: 'mdi-message-text', link: '/' },
        { title: 'Outreach', icon: 'mdi-contacts', link: '/outreach' },
        { title: 'Positions', icon: 'mdi-clipboard-list', link: '/positions' },
        { title: 'Candidates', icon: 'mdi-desktop-mac-dashboard', link: '/candidates' }
      ]
    }
  }
}
</script>
