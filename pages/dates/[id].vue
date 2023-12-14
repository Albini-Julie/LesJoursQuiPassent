<script setup>
import { useRoute } from "vue-router";
const route = useRoute();

const { data: recipe } = await useAsyncData("recipe", async () => {
  return $fetch(env.public.apiUrl + `/recipes/${route.params.id}`);
});
</script>
