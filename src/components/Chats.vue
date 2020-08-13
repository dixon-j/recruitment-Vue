<template>
  <v-container class="pa-0">
    <v-list v-if="loading">
        <v-list-item>
          <v-list-item-content>
            <v-sheet>
              <v-skeleton-loader
                type="list-item-avatar"
                max-width="300"
              ></v-skeleton-loader>
            </v-sheet>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    <v-list class="pa-0" v-else>
      <v-list-item>
        <v-list-item-avatar>
          <v-avatar :color="(currentCandidate.score >= 75)?'green': (currentCandidate.score >= 50)?'blue': (currentCandidate.score >= 25)? 'yellow darken-4' : 'red'"
            v-if="currentCandidate.avatar === undefined">
            <span class="white--text">{{getInitials(currentCandidate.name)}}</span>
          </v-avatar>
          <v-img :src="currentCandidate.avatar" v-else></v-img>
        </v-list-item-avatar>
        <v-list-item-content>
          {{currentCandidate.name}}
        </v-list-item-content>
      </v-list-item>
    </v-list>
    <div :style="{height:height,overflow:'auto',scrollbarWidth: 'thin'}" ref="chatlog">
      <v-list v-if="loading">
        <v-list-item v-for="item in dummy" :key="item">
          <v-list-item-content>
            <v-sheet>
              <v-skeleton-loader
                type="paragraph"
                tile
                max-width="200"
                :class="(item%2 == 0)?'ml-auto': 'mr-auto'"
              ></v-skeleton-loader>
            </v-sheet>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-list v-else>
          <v-list-item v-for="(item, index) in currentCandidate.chat" :key="index">
              <v-list-item-content>
                <v-row :justify="(item.sender==='user')?'start':'end'">
                  <v-card max-width="300" class="mx-3" dark :color="(item.sender==='bot')?'blue': 'green'">
                    <v-card-text class="white--text">
                      {{item.text}}
                    </v-card-text>
                  </v-card>
                </v-row>
              </v-list-item-content>
          </v-list-item>
      </v-list>
    </div>
      <v-divider></v-divider>
      <v-container class="py-0">
        <v-text-field
          v-model="message"
          append-outer-icon="mdi-send"
          prepend-icon="mdi-message"
          clear-icon="mdi-close-circle"
          clearable
          label="Message"
          type="text"
          :loading="sendLoading"
          @click:append-outer="sendChat"
        ></v-text-field>
      </v-container>
  </v-container>
</template>
<script>
import { mapState, mapActions } from 'vuex'
export default {
  data: () => ({
    sendLoading: false,
    message: '',
    dummy: [1, 2, 3, 4, 5, 6, 7, 8]
  }),
  computed: {
    ...mapState(['currentCandidate', 'loading']),
    height () {
      if (this.$vuetify.breakpoint.name === 'xl') {
        return '86vmin'
      }
      if (this.$vuetify.breakpoint.name === 'lg') {
        return '81vmin'
      }
      if (this.$vuetify.breakpoint.name === 'md') {
        return '38vmin'
      }
      if (this.$vuetify.breakpoint.name === 'sm') {
        return '28vmin'
      }
      return '45min'
    }
  },
  methods: {
    ...mapActions(['fetchNewChat', 'sendMessage']),
    scrollToEnd () {
      var chatlog = this.$refs.chatlog
      chatlog.scrollTop = chatlog.scrollHeight
    },
    sendChat () {
      if (this.message) {
        this.sendLoading = true
        this.sendMessage(this.message)
        this.message = ''
        setInterval(() => {
          this.sendLoading = false
        }, 2000)
      }
    },
    getInitials (string) {
      const names = string.split(' ')
      let initials = names[0].substring(0, 1).toUpperCase()
      if (names.length > 1) {
        initials += names[names.length - 1].substring(0, 1).toUpperCase()
      }
      return initials
    }
  },
  mounted () {
    this.scrollToEnd()
    setInterval(() => {
      this.fetchNewChat()
    }, 25000)
  },
  updated () {
    this.scrollToEnd()
  }
}
</script>
