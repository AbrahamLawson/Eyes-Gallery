<template>
  <section class="containerSearch flex items-center justify-center mt-10">
    <div class="cone icone-search flex-center">
      <img
        src="../assets/loupe.png"
        alt="icon-search"
        class="w-8 h-8 align-middle mr-4"
      />
    </div>
    <div class="input-search flex-center">
      <form>
        <input
          v-model="youtubeLink"
          placeholder="Entrer votre liens..."
          required
          class="border border-gray-300 rounded p-2"
        />
        <button class="search" @click="handleSubmit">Rechercher</button>
      </form>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      youtubeLink: "", // Initialisation de la variable pour stocker le lien YouTube
    };
  },

  methods: {
    // Methode pour gerer l'action de l'utilisateur par rapport à la soumissions
    handleSubmit() {
      // Conditions pour vérifier si le lien YouTube est non vide
      if (this.youtubeLink) {
        this.$emit("add-video", this.youtubeLink);
        this.youtubeLink = ""; // Je vide mon input
      } else {
        alert("Ce champs est requis, veuillez rentrer un liens ^^");
      }
    },
  },
});
</script>
<style scoped>
.search {
  margin: 5px;
  padding: 10px;
  border-radius: 10px;
  background: wheat;
  font-weight: 400;
  transition: transform 0.3s ease;
}
.search:hover {
  transform: scale(0.95);
}
</style>
