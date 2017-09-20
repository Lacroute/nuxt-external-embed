<template>
  <section class="container">
    <div>
      <logo/>
      <h1 class="title">
        nuxt-external-embed
      </h1>
      <button type="button" @click="increment({term: 2})">Increment from Nuxt</button>
      <external/>
    </div>
  </section>
</template>

<script>
import { mapMutations } from 'vuex'

import Logo from '~/components/Logo.vue'
// Making constants is important!
import { External, myModule, NAMESPACE, INCREMENT } from 'vue-external-component'

export default {
  components: {
    Logo,
    External
  },

  created () {
    // Connect the store from the component to the store of the Nuxt app.
    this.$store.registerModule(NAMESPACE, myModule)
  },

  destroyed () {
    // Remove it before leaving.
    this.$store.unregisterModule(NAMESPACE)
  },

  methods: {
    // Now, the tool is fully integrated and we can interact with.
    ...mapMutations(NAMESPACE, {
      increment: INCREMENT
    })
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
