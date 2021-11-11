<template>
  <article
    class="flex lg:h-screen w-screen lg:overflow-hidden xs:flex-col lg:flex-row"
  >
    <div class="relative lg:w-1/2 xs:w-full xs:h-84 lg:h-full post-left">
      <img
        :src="`/images/${experience.logo}`"
        alt="mobile"
        class="flex-no-shrink fill-current"
      />
      <div class="overlay"></div>
    </div>
    <div
      class="
        relative
        xs:py-8 xs:px-8
        lg:py-32 lg:px-16 lg:w-1/2
        xs:w-full
        h-full
        overflow-y-scroll
        markdown-body
        post-right
        custom-scroll
      "
    >
      <h1 class="text-3xl text-gray-700">{{ experience.job }}</h1>
      <h4 class="text-gray-600 text-base mb-10">{{ experience.dates }}</h4>
      <!-- content from markdown -->
      <nuxt-content :document="experience" />
      <!-- prevNext component -->
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