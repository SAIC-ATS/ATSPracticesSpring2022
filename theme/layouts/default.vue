<template>
  <div class="flex" :style="{ backgroundColor: menuBackground }">
    <!-- menu -->
    <div>
      <div
        class="relative w-24 text-center mr-2 hover:mt-0"
        id="open"
        @click="toggle"
      >
        <div :class="[isOpen ? 'hidden' : 'block']">
          <img class="ml-2 filter object-cover sepia-on-hover" src="tab.png" />
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
          <div class="w-48">
            <NuxLink to="/">
              <img class="filter sepia-on-hover" src="tab-b.png" />
              <font-awesome-icon
                :icon="['fas', 'bars']"
                class="
                  absolute
                  fa-lg
                  -ml-3
                  -top-7
                  h-24
                  w-24
                  pointer-events-none
                  text-slate-200
                  opacity-75
                "
              />
            </NuxLink>
          </div>
          <div v-for="student of students" :key="student.slug" class="w-48">
            <div v-if="student.content_type == 'page'" :style="student.color">
              <NuxtLink :to="student.slug" class="sticky right-0">
                <img class="filter sepia-on-hover" src="tab-b.png" />
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
            <div
              v-if="student.content_type == 'student' && student.url != null"
            >
              <NuxtLink :to="student.slug" class="sticky right-0">
                <img class="filter sepia-on-hover" src="tab-b.png" />
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
              <img class="filter sepia-on-hover" src="tab.png" />
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
    <!-- student content -->
    <Nuxt />
  </div>
</template>
<script>
export default {
  layout: "default",
  data() {
    return {
      isOpen: false,
      students: [],
    };
  },
  computed: {
    menuBackground() {
      let slug = this.$route.params.slug;
      if (slug && this.students.length) {
        let currentStudent = this.students.find((s) => s.slug == slug);
        return currentStudent.color;
      } else {
        return "#FFFFFF";
      }
    },
  },
  mounted() {
    // Get students
    this.getStudents().then((data) => {
      this.students = data;
    });
  },
  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
    },
    getStudents() {
      return this.$content()
        .only(["name", "position", "url", "color", "slug", "content_type"])
        .sortBy("position", "asc")
        .fetch();
    },
  },
};
</script>

<style>
/* Special classes that don't make sense in tailwind go here. */
.sepia-on-hover:hover {
  filter: sepia(100%);
}
</style>
