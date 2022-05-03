<template>
  <div class="flex justify-between">
    <!-- menu -->
    <div
      class="relative w-24 text-center mr-2 hover:mt-0"
      id="open"
      @click="toggle"
    >
      <div :class="[isOpen ? 'hidden' : 'block']">
        <img class="ml-2 filter object-cover hover:sepia" src="tab.png" />
        <font-awesome-icon
          :icon="['fas', 'bars']"
          class="
            absolute
            fa-lg
            -ml-1
            -top-9
            h-24
            w-24
            pointer-events-none
            text-slate-200
            opacity-75
          "
        />
      </div>
      <div :class="[isOpen ? 'block' : 'hidden']" class="mb-6 z-50">
        <div v-for="student of students" :key="student.slug" class="w-48">
          <div v-if="student.content_type == 'page'">
            <NuxtLink :to="student.slug" class="sticky right-0">
              <img class="filter hover:sepia" src="tab-b.png" />
              <p
                class="
                  absolute
                  pointer-events-none
                  index-x-0
                  top-4
                  w-52
                  uppercase
                  text-slate-200
                  opacity-75
                "
              >
                {{ student.name }}
              </p>
            </NuxtLink>
          </div>
          <div v-if="student.content_type == 'student'">
            <NuxtLink :to="student.slug" class="sticky right-0">
              <img class="filter hover:sepia" src="tab-b.png" />
              <p
                class="
                  absolute
                  pointer-events-none
                  index-x-0
                  top-4
                  w-52
                  uppercase
                  text-slate-200
                  opacity-75
                "
              >
                {{ student.name }}
              </p>
            </NuxtLink>
          </div>
        </div>

        <div class="w-48">
          <NuxtLink to="/" class="sticky right-0">
            <img class="filter hover:sepia" src="tab.png" />
            <p
              class="
                absolute
                pointer-events-none
                index-x-0
                top-4
                w-52
                uppercase
                text-slate-200
                opacity-75
              "
            >
              Home
            </p>
          </NuxtLink>
        </div>
      </div>
    </div>
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
    const students = await $content()
      .only([
        "title",
        "name",
        "position",
        "url",
        "img",
        "color",
        "slug",
        "content_type",
      ])
      .sortBy("position", "asc")
      .fetch();
    return {
      doc,
      students,
    };
  },
};
</script>
