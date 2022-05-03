<template>
  <div>
    <div>
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
    </div>
    <div class="sticky bottom-0 pointer-events-none">
      <!-- folder -->
      <img src="art&tech_folder.png" class="w-1/3 h-1/3 mx-auto" />
      <!-- credits -->
      <div class="z-0 m-12 md:grid md:grid-cols-8 gap-4 text-sm">
        <h4 class="font-bold md:text-center my-4 md:my-0">Instructors:</h4>
        <p>Garrett Laroy Johnson</p>
        <p>Kristin McWharter</p>
        <h4 class="font-bold md:text-right my-4 md:my-0">TA:</h4>
        <p>Sara Niroobakhsh</p>
        <h4 class="font-bold md:text-right my-4 md:my-0">Lab Techs:</h4>
        <p>Blake Fall-Conroy</p>
        <p class="mr-5">Juan Eduardo Flores</p>
      </div>
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
    const students = await $content(params.slug)
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
      students,
    };
  },
};
</script>
