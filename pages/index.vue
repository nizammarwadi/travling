<template>
  <div>
      <Review/>
      <Card/>
  </div>
</template>

<script>
import Review from "~/components/organisms/Review.vue"
import Card from "~/components/organisms/Card.vue"
export default {
  components: {
    Review: Review,
    Card: Card,
  }
}
</script>

<style>
  

</style>