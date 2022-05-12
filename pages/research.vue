<template>
  <div>
    <!-- <div class="m-24">
      <img src="observations.png" class="" />
    </div> -->
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
