<template>
  <div class="container flex flex-col justify-center text-center items-center">
    <h1 class="mb-4 text-xl">
      When we get out of Lockdown this is what I need to eat
    </h1>
    <TheTable />
  </div>
</template>

<script>
import TheTable from '~/components/TheTable.vue'

export default {
  components: {
    TheTable
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
}
</style>
