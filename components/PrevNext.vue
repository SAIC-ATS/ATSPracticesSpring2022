<template>
  <div class="flex">
    <div class="flex flex-grow justify-between">
      <NuxtLink
        v-if="prev"
        :to="{ params: { slug: prev.slug } }"
        class="
          relative
          w-40
          font-bold
          text-primary text-center text-sm
          -mt-8
          hover:mt-0
        "
      >
        <img
          class="rotate-90 ml-16 -mt-16 w-11 filter sepia-on-hover"
          src="tab.png"
        />
        <p
          class="
            absolute
            top-2
            inset-x-0
            pointer-events-none
            uppercase
            text-slate-200
            opacity-75
          "
        >
          {{ prev.name }}
        </p>
      </NuxtLink>
      <span v-else>&nbsp;</span>
      <NuxtLink
        v-if="next"
        :to="{ params: { slug: next.slug } }"
        class="
          relative
          mr-16
          w-40
          font-bold
          text-primary text-sm text-center
          -mt-8
          hover:mt-0
        "
      >
        <img
          class="rotate-90 ml-14 -mt-16 w-11 filter sepia-on-hover"
          src="tab.png"
        />
        <p
          class="
            absolute
            top-2
            inset-x-0
            pointer-events-none
            uppercase
            text-slate-200
            opacity-75
          "
        >
          {{ next.name }}
        </p></NuxtLink
      >
      <span v-else>&nbsp;</span>
    </div>
    <div
      class="relative w-10 text-center mr-2 hover:mt-0 -mt-5"
      id="open"
      @click="toggle"
    >
      <img
        class="rotate-90 ml-4 -mt-16 filter object-cover sepia-on-hover"
        src="tab.png"
      />
      <font-awesome-icon
        :icon="['fas', 'bars']"
        class="
          absolute
          top-2
          inset-x-0
          pointer-events-none
          text-slate-200
          opacity-75
        "
      />
      <TabMenu :class="[isOpen ? 'block' : 'hidden']" />
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
  props: {
    prev: {
      type: Object,
      default: () => null,
    },
    next: {
      type: Object,
      default: () => null,
    },
  },
};
</script>
