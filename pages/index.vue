<template>
  <div>
    <!-- <v-btn color="blue" dark @click="sheet = !sheet"> Open v-model </v-btn>
    <v-bottom-sheet v-model="sheet">
      <v-sheet class="text-center" height="200px">
        <v-btn class="mt-6" text color="red" @click="sheet = !sheet">
          close
        </v-btn>
        <div class="py-3">
          This is a bottom sheet using the controlled by v-model instead of
          activator
        </div>
      </v-sheet>
    </v-bottom-sheet> -->
    {{ epg }}
    {{ err }}
  </div>
</template>

<script>
export default {
  fetch() {
    this.$axios
      .get(
        "https://portal2.teleosmedia.com/epg/?channel_id=journy&client_id=ovation&days=2"
      )
      .then(({ data }) => (this.epg = data))
      .catch((err) => (this.err = err));
  },
  data() {
    return {
      epg: {},
      err: "",
      sheet: false,
      tiles: [
        { img: "keep.png", title: "Keep" },
        { img: "inbox.png", title: "Inbox" },
        { img: "hangouts.png", title: "Hangouts" },
        { img: "messenger.png", title: "Messenger" },
        { img: "google.png", title: "Google+" },
      ],
    };
  },
};
</script>

<style lang="scss">
.v-overlay.v-overlay--active {
  backdrop-filter: saturate(180%) blur(10px) !important;
  background-color: rgba(black, 0.8) !important;
  opacity: 1 !important;
}
.v-menu__content {
  top: unset !important;
  min-width: 100vw !important;
  bottom: 0 !important;
  left: 0 !important;
  position: fixed !important;

  .v-list.v-sheet {
    border-radius: 1rem 1rem 0 0 !important;
    position: relative;
  }
}
</style>