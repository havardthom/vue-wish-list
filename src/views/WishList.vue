<template>
  <v-container>
    <v-row
      justify="center"
    >
      <v-col cols="8">
        <wish-list />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import WishList from "@/components/WishList"

export default {
  components: { WishList }
}
</script>