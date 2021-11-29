<template>
  <div>
    <div
      class="
        hero
        container-inner
        mx-auto
        flex flex-col
        sm:flex-row
        justify-between
        py-16
      "
    >
      <div class="text-4xl font-bold w-full sm:w-3/5 text-center sm:text-left">
        <div class="text-green-700 leading-tight">
          QA Ingénieur &amp; Développeur Front
        </div>
      </div>
      <div class="mt-8 sm:mt-0">
        <img
          src="~assets/img/photo-profil.jpeg"
          alt="hero"
          class="w-32 h-32 rounded-full mx-auto sm:mx-0"
        />
      </div>
    </div>
    <!-- end hero -->

    <div class="container-inner mx-auto mb-16">
      <p class="text-lg sm:text-xl">
        Diplômé de l'ESIEA, école d'ingénieur à Ivry-sur-Seine, je travaille
        depuis plus de 7 ans dans le monde de la qualité.
      </p>
      <p class="text-lg sm:text-xl">
        Spécialisé en automatisation de tests et développement d'outils de
        tests, je cherche à présent à m'orienter vers le développement Front
        (Web et Mobile), tout en gardant une forte appétence pour la qualité et
        son amélioration perpétuelle dans les projets sur lesquels j'interviens.
      </p>
    </div>

    <div class="overflow-x-hidden">
      <div
        class="
          projects
          container-inner
          mx-auto
          text-xl
          border-t border-gray-500
          py-16
          relative
        "
      >
        <h2 class="font-bold mb-6" id="journey">Mon parcours :</h2>

        <ul class="text-lg sm:text-xl space-y-6">
          <li v-for="experience of experiences" :key="experience.slug">
            <NuxtLink
              :to="{
                name: 'experiences-slug',
                params: { slug: experience.slug },
              }"
            >
              <div class="flex">
                <img
                  :src="`/images/${experience.logo}`"
                  alt="mobile"
                  class="h-11 w-11 flex-no-shrink fill-current logo mr-5"
                />
                <div class="flex flex-col justify-center">
                  <h3>{{ experience.title }}</h3>
                  <h4 class="text-gray-600 text-base">
                    {{ experience.dates }}
                  </h4>
                  <div class="text-lg text-gray-700">
                    {{ experience.job }}
                  </div>
                </div>
              </div>
            </NuxtLink>
          </li>
        </ul>
      </div>
      <!-- end journey -->
    </div>

    <div class="overflow-x-hidden">
      <div
        class="
          projects
          container-inner
          mx-auto
          text-xl
          border-t border-gray-500 border-b
          py-16
          mb-16
          relative
        "
      >
        <h2 class="font-bold mb-6" id="projects">Mes projets :</h2>
        <ul class="text-lg sm:text-xl space-y-6">
          <li v-for="project of projects" :key="project.slug">
            <NuxtLink
              :to="{ name: 'projects-slug', params: { slug: project.slug } }"
            >
              <div class="flex">
                <img
                  :src="`/images/${project.logo}`"
                  alt="mobile"
                  class="w-11 flex-no-shrink fill-current logo mr-5"
                />
                <div class="flex flex-col justify-center">
                  <h3>{{ project.title }}</h3>
                  <div class="text-lg text-gray-700">
                    {{ project.description }}
                  </div>
                </div>
              </div>
            </NuxtLink>
          </li>
        </ul>
      </div>
      <!-- end projects -->
    </div>

    <div class="overflow-x-hidden border-gray-200 border-b">
      <div
        class="get-to-know-me container-inner mx-auto text-xl pb-16 relative"
      >
        <h2 class="font-bold mb-6" id="hobbies">Mes loisirs :</h2>

        <ul class="text-lg sm:text-xl space-y-6">
          <li v-for="hobby of hobbies" :key="hobby.slug">
            <div class="flex">
              <div class="flex flex-row justify-center">
                <img
                  :src="`/images/${hobby.icon}`"
                  alt="logo hobby"
                  class="flex-no-shrink fill-current logo mr-5"
                />
                <v-icon large color="green darken-2"> mdi-domain </v-icon>
                <div class="flex flex-col">
                  <div v-for="item of hobby.items" :key="item">
                    <span class="text-xl text-gray-700">{{ item.name }}</span>
                    <span class="text-lg text-gray-600">{{
                      item.description
                    }}</span>
                  </div>
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
      <!-- end get-to-know me -->
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const projects = await $content("projects")
      .only(["title", "description", "img", "slug", "logo"])
      .sortBy("createdAt", "asc")
      .fetch();

    const experiences = await $content("experiences")
      .only(["title", "job", "img", "slug", "logo", "dates"])
      .sortBy("createdAt", "asc")
      .fetch();

    const hobbies = await $content("hobbies")
      .sortBy("createdAt", "asc")
      .fetch();

    return {
      projects,
      experiences,
      hobbies,
    };
  },
};
</script>

<style>
</style>
