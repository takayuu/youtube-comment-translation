<template>
  <v-app-bar color="red" app clipped-left>
    <v-app-bar-nav-icon @click.stop="$emit('openDrawerMenu')">
      <v-icon>mdi-cog-outline</v-icon>
    </v-app-bar-nav-icon>
    <div class="ml-1">
      <img
        class="logo"
        src="../../static/logo.png"
        alt="YouTube Comment Translation"
      />
    </div>
    <v-spacer />
    <form
      @submit.prevent="sendURL"
      class="form d-none d-sm-block"
      autocomplete="off"
    >
      <v-text-field
        v-model="url"
        label="YouTube URL"
        append-icon="mdi-magnify"
        outlined
        hide-details
        dense
        color="#fff"
      />
    </form>
    <v-btn
      @click="openSearchArea"
      icon
      fab
      color="white"
      class="d-block d-sm-none"
    >
      <v-icon>mdi-magnify</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  name: "TheHeader",
  data() {
    return {
      url: ""
    };
  },
  methods: {
    sendURL() {
      const pattern = new RegExp("v=[0-9a-zA-Z\\-]{11}(&|$)");
      const result = pattern.test(this.url);

      if (result) {
        const videoId = this.url.match(pattern)[0].replace("v=", "");

        this.$nuxt.$emit("EVENT_SEND_URL", videoId);
      } else {
        this.$nuxt.$emit("EVENT_URL_ERROR", true);
      }
    },
    openSearchArea() {
      this.$nuxt.$emit("EVENT_OPEN_SEARCH", true);
    }
  }
};
</script>

<style scoped lang="scss">
.logo {
  width: auto;
  height: 35px;
  vertical-align: middle;
}

.form {
  display: block;
  max-width: 350px;
  width: 100%;
}
</style>
