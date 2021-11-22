<template>
  <article
    class="flex lg:h-screen w-screen lg:overflow-hidden xs:flex-col lg:flex-row"
  >
    <div class="relative lg:w-1/2 xs:w-full xs:h-84 lg:h-full post-left">
      <img
        :src="require(`~/assets/img/${project.img}`)"
        :alt="project.alt"
        class="absolute w-full object-cover"
      />
    </div>
    <div
      class="
        relative
        xs:py-8 xs:px-8
        lg:px-16
        xs:w-full
        h-full
        overflow-y-scroll
        post-right
        custom-scroll
        lg:w-1/2
      "
    >
      <div>
        <h1 class="text-3xl text-gray-700 mb-5">{{ project.title }}</h1>
        <h4 class="text-gray-600 text-xl mb-5">{{ project.description }}</h4>

        <div class="flex flex-row justify-around mb-10">
          <a
            :href="project.link"
            target="_blank"
            class="flex flex-row items-center"
          >
            <img
              src="~/assets/img/external-link.svg"
              alt="github logo"
              class="h-10 mr-3"
            />
            <span class="text-lg text-gray-700"> Découvrir </span>
          </a>
          <a
            :href="project.github"
            target="_blank"
            class="flex flex-row items-center"
          >
            <img
              src="~/assets/img/github.svg"
              alt="github logo"
              class="h-10 mr-3"
            />
            <span class="text-lg text-gray-700"> Repo Github </span>
          </a>
        </div>
        <div class="text-lg text-gray-700 mb-10">
          <nuxt-content :document="project" />
        </div>
        <li v-for="subject of project.subjects" :key="subject">
          <ul class="flex flex-row items-center mb-3">
            <img
              src="~/assets/icons/bullet.svg"
              alt="Bullet point"
              class="mr-3 h-3"
            />
            <div class="text-base text-gray-600">
              {{ subject }}
            </div>
          </ul>
        </li>
        <div>
          <div class="flex flex-row mt-10 mb-5">
            <img
              src="~/assets/icons/code.svg"
              alt="Code icon"
              class="mr-3"
            />
            <h3 class="text-xl text-gray-700">Stack :</h3>
          </div>
          <div class="flex flex-row flex-wrap">
            <div
              v-for="tool of project.tools"
              :key="tool"
              class="flex flex-col items-center mr-5"
            >
              <img :src="`/images/${tool.logo}`" alt="mobile" class="h-10" />
              <span class="text-lg text-gray-700">
                {{ tool.name }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </article>
</template>
<script>
export default {
  async asyncData({ $content, params }) {
    const project = await $content("projects", params.slug).fetch();
    // const tagsList = await $content('tags')
    //   .only(['name', 'slug'])
    //   .where({ name: { $containsAny: project.tags } })
    //   .fetch()
    // const tags = Object.assign({}, ...tagsList.map((s) => ({ [s.name]: s })))
    const [prev, next] = await $content("projects")
      .only(["title", "slug"])
      .sortBy("createdAt", "asc")
      .surround(params.slug)
      .fetch();
    return {
      project,
      // tags,
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
li {
  list-style-type: none;
}
</style>