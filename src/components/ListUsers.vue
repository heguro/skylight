<script setup lang="ts">
import TileUser from "@/components/TileUser.vue";
import { getMyFollowers, getMyFollows } from "@/lib/atp";
import { PropType } from "vue";

const props = defineProps({
  kind: {
    type: String as PropType<"follows" | "followers">,
    required: true,
  },
});

const users =
  props.kind === "follows"
    ? (await getMyFollows()).follows
    : (await getMyFollowers()).followers;
</script>

<template>
  <TileUser
    v-for="user in users"
    :user="user"
    :key="user.handle"
    class="py-2 my-2"
  />
</template>
