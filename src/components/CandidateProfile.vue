<template>
<div :style="{maxHeight:height,overflow:'auto'}" class="fill-height">
  <v-container>
    <v-card flat>
        <v-card-actions class="mb-8">
        <!-- <v-row justify="space-around">
        <v-btn color="success" dark>Accept</v-btn>
        <v-btn color="error" dark>Reject</v-btn>
        </v-row> -->
      </v-card-actions>
      <v-row justify="center" align="center">
      <v-progress-circular
        :value= currentCandidate.score
        size= 175
        rotate="48"
        :indeterminate="loading"
        :color= "(currentCandidate.score >= 75)?'green': (currentCandidate.score >= 50)?'blue': (currentCandidate.score >= 25)? 'yellow darken-4' : 'red'"
      >
      <v-badge
          :content= currentCandidate.score
          :color="(currentCandidate.score >= 75)?'green': (currentCandidate.score >= 50)?'blue': (currentCandidate.score >= 25)? 'yellow darken-4' : 'red'"
          bottom
          label
          tile
          offset-x="12"
          offset-y="12"
          v-if="!loading"
        >
      <v-avatar size="150">
        <span class="text-h2" v-if="currentCandidate.avatar === undefined">{{getInitials(currentCandidate.name)}}</span>
        <img
          :src=currentCandidate.avatar
          :alt=currentCandidate.name
          v-else
        >
      </v-avatar>
      </v-badge>
      </v-progress-circular>
      </v-row>
      <div class="display-1 text-center mt-5 mb-2" v-if="!loading">{{ currentCandidate.name }}</div>
      <v-card-subtitle class="text-center pt-0" v-if="!loading"><v-icon size="medium">mdi-phone-outgoing</v-icon> {{currentCandidate.phone}}</v-card-subtitle>
      <v-row justify="space-around" class="mb-5" v-if="!loading">
          <v-btn
            color="blue"
            class="white--text"
          >
            Resume
            <v-icon> mdi-download </v-icon>
          </v-btn>
      </v-row>
      <v-textarea outlined label="Notes" v-model="note" v-if="!loading">
      </v-textarea>
      <v-row justify="center" class="mt-0 mb-12 mr-2" v-if="!loading">
        <v-btn
          color="warning"
          class="white--text"
          @click="postNotes(currentCandidate._id)"
          :loading="saving"
          :disabled="saving"
        >
          Save
          <v-icon> mdi-content-save </v-icon>
        </v-btn>
      </v-row>
        <v-alert :type="save" dense v-if="msg">
          {{msg}}
        </v-alert>
    </v-card>
  </v-container>
  </div>
</template>
<script>
import { mapState, mapActions } from 'vuex'
export default {
  data: () => ({
    note: '',
    saving: false,
    save: '',
    msg: ''
  }),
  computed: {
    ...mapState(['currentCandidate', 'loading']),
    height () {
      if (this.$vuetify.breakpoint.name === 'xl') {
        return '100vmin'
      }
      if (this.$vuetify.breakpoint.name === 'lg') {
        return '100vmin'
      }
      if (this.$vuetify.breakpoint.name === 'md') {
        return '62vmin'
      }
      return '60vmin'
    }
  },
  watch: {
    currentCandidate () {
      this.note = this.currentCandidate.notes
    },
    msg () {
      if (this.msg) {
        setTimeout(() => {
          this.msg = ''
        }, 3000)
      }
    }
  },
  methods: {
    ...mapActions(['addNotes']),
    getInitials (string) {
      const names = string.split(' ')
      let initials = names[0].substring(0, 1).toUpperCase()
      if (names.length > 1) {
        initials += names[names.length - 1].substring(0, 1).toUpperCase()
      }
      return initials
    },
    async postNotes (id) {
      this.saving = true
      const notes = {
        id: id,
        text: this.note
      }
      await this.addNotes(notes)
      if (this.currentCandidate.notes === this.note) {
        this.msg = 'Save Successful'
        this.save = 'success'
        this.saving = false
      } else {
        this.msg = 'Saving Failed'
        this.save = 'error'
        this.saving = false
      }
    }
  }
}
</script>
