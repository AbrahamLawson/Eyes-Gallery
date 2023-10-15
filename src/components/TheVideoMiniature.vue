<template>
  <div class="video-container">
    <div class="video-thumbnail" @click="openVideo">
      <img :src="thumbnail" alt="Miniature de la vidéo" />
    </div>
    <button @click="deleteVideo" class="delete-button">Supprimer</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    thumbnail: {
      type: String,
      required: true,
    },
    videoLink: {
      type: String,
      required: true,
    },
    videoIndex: {
      type: Number,
      required: true,
    },
  },
  // Methode pour gerer l'action de l'utilisateur par rapport à la soumissions

  methods: {
    openVideo() {
      window.open(this.videoLink);
    },
    deleteVideo() {
      this.$emit("remove-video", this.videoIndex);
    },
  },
});
</script>

<style scoped>
.video-container {
  box-shadow: -20px 20px 20px 2px;
  transition: filter 0.4s ease-out;
  cursor: pointer;
  margin: 10px;
}

.video-container :hover {
  filter: drop-shadow(0px 0px 20px gold);
}

.delete-button {
  margin: 20px;
  padding: 10px;
  background: rgb(252, 252, 252);
  border-radius: 10px;
}
.delete-button:hover {
  background: red;
  filter: drop-shadow(0px 0px 20px red);
}
</style>
