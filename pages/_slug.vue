<template>
  <div class="w-full">
    <div class="flex w-full" :style="doc.color">
      <iframe
        :src="doc.url"
        class="h-screen w-full"
        style="margin-top: -60px; height: calc(100vh + 12rem)"
        id="iframe"
        frameborder="0"
        allow="camera https://editor.p5js.org; microphone https://editor.p5js.org"/>
      ></iframe>
    </div>
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
