<template>

  <div>
    <div v-show="loaded">
      {{ $localStorageLoaded }}
      {{ $sessionStorageLoaded }}
      {{ $store.state.localStorage.anyValues }}
      {{ $store.state.sessionStorage.anyValues }}
    </div>

    <div class="m-3">
      <div>{{anyValues}}</div>
      <button @click="increment">喜加一</button>

    </div>

    <div class="m-3 flex-none">
      <button class="px-3 py-1 bg-blue-500 border rounded shadow-2xl text-white text-sm flex-none"><a href="/new/thetext1">
          OK Confirm
        </a></button>
    </div>

  </div>
</template>

<script>
import { mapState } from 'vuex'
import { mapMutations } from 'vuex'

export default {
  computed: {
    loaded() {
      return (
        this.$store.state.localStorage.status &&
        this.$store.state.sessionStorage.status
      )
    },

    ...mapState({
      anyValues: (state) => state.localStorage.anyValues,
    }),
  },

  methods: {
    ...mapMutations({
      increment: 'increment',
    }),
  },
}
</script>