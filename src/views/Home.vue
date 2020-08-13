<template>
  <v-row no-gutters class="fill-height">
    <v-snackbar
      v-model="snackbar"
      color="error"
      app
      left
      multi-line
      top
    >
    {{errorMsg}}
      <template v-slot:action="{ attrs }">
        <v-btn
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
    <v-col xl="2" lg="2" md="6" sm="6" class="divide" fill-height>
      <Vacancies/>
    </v-col>
    <v-col xl= "3" lg="3" md="6" sm="6" class="divide" fill-height>
      <Candidates/>
    </v-col>
    <v-col xl= "4" lg="4" md="8" sm="12" cols="12" class="divide" >
      <Chats/>
    </v-col>
    <v-col xl= "3" lg="3" md="4" sm="12" cols="12">
      <CandidateProfile/>
    </v-col>
  </v-row>
</template>

<script>
// @ is an alias to /src
import Vacancies from '@/components/Vacancies.vue'
import Candidates from '@/components/Candidates.vue'
import Chats from '@/components/Chats.vue'
import CandidateProfile from '@/components/CandidateProfile.vue'
import { mapState } from 'vuex'

export default {
  name: 'Home',
  components: {
    Vacancies,
    Candidates,
    Chats,
    CandidateProfile
  },
  data: () => ({
    snackbar: false,
    errorMsg: ''
  }),
  computed: {
    ...mapState(['globalError'])
  },
  watch: {
    globalError () {
      if (this.globalError) {
        this.errorMsg = this.globalError
        this.snackbar = true
      }
    }
  }
}
</script>
<style>
.divide {
  border-right: 1px solid lightgray;
}
::-webkit-scrollbar {
  width: 10px;
}
::-webkit-scrollbar-track {
  background: #f1f1f1;
}
::-webkit-scrollbar-thumb {
  background: lightgray;
}
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>
