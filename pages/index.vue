<template>
  <div>
    <!--Vidéo-->
    <div @click="startVideoPlayback">
      <div ref="videoContainer" class="video-container">
        <video ref="videoRef">
          <source :src="videoSource" type="video/mp4" />
        </video>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    const videoContainer = ref(null);
    const videoRef = ref(null);
    const videoSource = ref("/FLEURS_BLANCHES.mp4");
    let observer;

    const handleIntersection = (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          // L'élément vidéo est visible, ajustez la vitesse de lecture
          videoRef.value.playbackRate = entry.intersectionRatio; // Ajustez la vitesse en fonction de la partie visible
        }
      });
    };

    const startVideoPlayback = () => {
      if (videoRef.value) {
        videoRef.value.play();
      }
    };

    onMounted(() => {
      // Créer un observateur d'intersection
      observer = new IntersectionObserver(handleIntersection, {
        threshold: [0, 0.5, 1],
      });

      // Observer l'élément vidéo
      observer.observe(videoContainer.value);
    });

    return {
      videoContainer,
      videoRef,
      videoSource,
      startVideoPlayback,
    };
  },
};
</script>

<style scoped>
.video-container {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: black; /* Couleur de fond pendant le défilement */
  overflow: hidden;
}

video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
