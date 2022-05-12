<template>
  <div class="m-28">
    <div class="absolute top-0 w-full h-44 bg-white">
      <p class="m-24 font-bold text-2xl">
        Art & Tachnology Practices: Spring 2022
      </p>
    </div>
    <iframe
      class="my-5 h-96 w-full"
      src="https://editor.p5js.org/kmcwha/full/wZLfo3-ja"
    ></iframe>
    <p class="mx-10">
      Art & Technology Practices is a team-taught, introductory course that
      provides a foundation for coursework in the Art and Technology Studies
      department at SAIC. Students are given a broad interdisciplinary grounding
      in the skills, concepts, and hands-on experiences they will need to engage
      the potentials of new technologies in art making. Together, we will
      explore the creative use of technology as a medium. Every other week, a
      lecture and discussion group exposes students to concepts of electronic
      media, perception, inter-media composition, emerging venues, and other
      issues important to artists working with technologically based media.
      Students will attend a morning & afternoon section each day to gain
      hands-on experience with a variety of forms and techniques central to
      technologically based art making.
    </p>
    <p class="mx-10">
      This semester students deleoped a collective imaginging of a specualtive
      class doppleganger based upon a series of experiments, playtests, and
      inquiries with our relationships to technology. We began by averaging our
      shared idea of where "home" is located and found that this particular
      collective's average location is somewhere near here:
    </p>
    <img class="my-6" src="averagelocation.png" />
    <p class="mx-10">
      From here we spent the semester researching to better understand where we
      are, where we have been, and where we are going. Using our skills and
      beliefs about technology to guide us in imagining what may be in store for
      our future.
    </p>
    <img class="my-6" src="observations.png" />
    <!-- <NuxtLink to="research">
      <p class="m-10 font-bold hover:text-red-500">Our research...</p>
    </NuxtLink> -->
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const doc = await $content("about").fetch();
    return {
      doc,
    };
  },
};
</script>
