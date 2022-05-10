<template>
  <div class="flex justify-between">
    <h1 class="mx-auto mt-24">COMING SOON!</h1>
    <nuxt-content :document="doc" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
    },
  },
  async asyncData({ $content, params }) {
    const doc = await $content(params.slug).fetch();

    return {
      doc,
    };
  },
};
</script>
