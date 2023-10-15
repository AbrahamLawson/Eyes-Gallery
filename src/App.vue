<template>
  <div class="bg-cover bg-center">
    <TheHeader />
    <main class="h-screen bg-opacity-50">
      <div>
        <TheVideoInput @add-video="addVideo"></TheVideoInput>
        <div class="thumbnails-container">
          <TheVideoMiniature
            v-for="(video, index) in videos"
            :key="index"
            :thumbnail="video.thumbnail || ''"
            :video-link="video.link"
            :video-index="index"
            @remove-video="removeVideo"
          ></TheVideoMiniature>
        </div>
      </div>
    </main>
    <router-view />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TheHeader from "./components/TheHeader.vue";
import TheVideoInput from "./components/TheVideoInput.vue";
import TheVideoMiniature from "./components/TheVideoMiniature.vue";
export default defineComponent({
  components: {
    TheHeader,
    TheVideoInput,
    TheVideoMiniature,
  },

  // Initialisation de la donnée "videos" comme un tableau vide
  data() {
    return {
      videos: [] as { link: string; thumbnail: string }[],
      error: null,
    };
  },

  methods: {
    addVideo(videoLink: string) {
      const apiUrl = `https://noembed.com/embed?url=${encodeURIComponent(
        videoLink
      )}`;

      //récupérer les datas avec fetch et gérer les different cas
      fetch(apiUrl)
        .then((response) => {
          if (!response.ok) {
            throw new Error(
              "Erreur lors de la récupération de la miniature. Vérifiez le lien."
            );
          }
          return response.json();
        })
        .then((data) => {
          const thumbnail = data.thumbnail_url;
          this.videos.push({ link: videoLink, thumbnail });
        })
        //catch les erreur et les afficher
        .catch((error) => {
          console.error(
            "Erreur lors de la récupération de la miniature :",
            error.message
          );
          alert("Le lien est introuvable. Veuillez vérifier et réessayer.");
        });
    },

    removeVideo(index: number) {
      if (index >= 0 && index < this.videos.length) {
        this.videos.splice(index, 1);
      }
    },
  },
});
</script>

<style>
body {
  background-image: url("./assets/background.svg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.thumbnails-container {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 80px;
}
</style>
