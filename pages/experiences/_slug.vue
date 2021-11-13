<template>
  <article
    class="flex lg:h-screen w-screen lg:overflow-hidden xs:flex-col lg:flex-row"
  >
    <div
      class="
        relative
        xs:py-8 xs:px-8
        lg:px-16
        xs:w-full
        h-full
        overflow-y-scroll
        markdown-body
        post-right
        custom-scroll
      "
    >
      <img :src="`/images/${experience.logo}`" alt="mobile" class="h-24 mb-10" />
      <div>
        <h1 class="text-3xl text-gray-700">{{ experience.job }}</h1>
        <h4 class="text-gray-600 text-base mb-10">{{ experience.dates }}</h4>
        <div class="text-lg text-gray-700 mb-10">
          <nuxt-content :document="experience" />
        </div>
        <div>
        <div class="flex flex-row mb-5">
          <img
            src="~/assets/icons/code.svg"
            alt="Right arrow bullet point"
            class="mr-3"
          />
          <h3 class="text-xl text-gray-700">Stack :</h3>
        </div>
        <div class="flex flex-row flex-wrap">
          <span
            v-for="tool of experience.tools"
            :key="tool"
            class="text-lg text-gray-700 mr-5"
          >
            {{ tool }}
          </span>
        </div>
      </div>
      </div>
    </div>
    <div
      class="
        xs:py-8 xs:px-8
        lg:py-40 lg:w-1/2
        xs:w-full
        h-full
        overflow-y-scroll
        mr-20
      "
    >
      <div class="flex flex-row mb-5">
        <img
          src="~/assets/icons/code.svg"
          alt="Right arrow bullet point"
          class="mr-3"
        />
        <h3 class="text-xl text-gray-700">Sujets traîtés :</h3>
      </div>

      <ul class="text-lg sm:text-xl space-y-6 mb-10">
        <li v-for="subject of experience.subjects" :key="subject">
          <div class="flex flex-row">
            <img
              src="~/assets/icons/right-arrow.svg"
              alt="Right arrow bullet point"
              class="mr-3"
            />
            <div class="text-base text-gray-600">
              {{ subject }}
            </div>
          </div>
        </li>
      </ul>

      <PrevNext :prev="prev" :next="next" class="mt-8" />
    </div>
  </article>
</template>
<script>
export default {
  async asyncData({ $content, params }) {
    const experience = await $content("experiences", params.slug).fetch();

    // const tagsList = await $content("tags")
    //   .only(["name", "slug"])
    //   .where({ name: { $containsAny: project.tags } })
    //   .fetch();
    // const tags = Object.assign({}, ...tagsList.map((s) => ({ [s.name]: s })));

    const [prev, next] = await $content("experiences")
      .only(["title", "slug"])
      .sortBy("createdAt", "asc")
      .surround(params.slug)
      .fetch();
    return {
      experience,
      prev,
      next,
    };
  },
  methods: {
    formatDate(date) {
      const options = { year: "numeric", month: "long", day: "numeric" };
      return new Date(date).toLocaleDateString("en", options);
    },
  },
};
</script>
<style>
.nuxt-content p {
  margin-bottom: 20px;
}
.nuxt-content h2 {
  font-weight: bold;
  font-size: 28px;
}
.nuxt-content h3 {
  font-weight: bold;
  font-size: 22px;
}
.icon.icon-link {
  display: inline-block;
  width: 20px;
  height: 20px;
  background-size: 20px 20px;
}
</style>