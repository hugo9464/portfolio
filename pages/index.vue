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
        <!-- <div class="leading-tight">Hugo Faye</div> -->
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
        Spécialisé en automatisation de tests et débeloppement d'outils de
        tests, je cherche à présent à m'orienter vers le développement Front
        (Web et Mobile), tout en gardant une forte appétence pour la qualité et
        son amélioration perpétuelle dans les projets sur lesquels j'interviens.
      </p>
      <!-- <div class="flex justify-between items-center py-6">
        <div class="w-full sm:w-1/2 px-8 py-8 sm:py-0">
          <img src="~assets/img/mind_map.svg" alt="browser" />
        </div>
        <div class="w-1/2 px-8 hidden sm:flex justify-end">
          <img src="~assets/img/code_review.svg" alt="mobile" />
        </div>
      </div> -->
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
          <li>
            <div class="flex">
              <img
                src="~assets/img/leboncoin.svg"
                alt="mobile"
                class="h-11 w-11 flex-no-shrink fill-current logo mr-5"
              />
              <div class="flex flex-col justify-center">
                <h3>QA Engineer</h3>
                <p class="text-base text-gray-600">Janvier 2019 - Août 2021</p>
                <div class="text-lg text-gray-600">
                  Lorem ipsum dolor sit amet consectetur adipisicing elit. Qui
                  ab nam animi iure nemo exercitationem a, eius non culpa
                  itaque!
                </div>
              </div>
            </div>
          </li>
          <li>
            <div class="flex">
              <img
                src="~assets/img/oui_sncf.svg"
                alt="mobile"
                class="h-11 w-11 flex-no-shrink fill-current logo mr-5"
              />
              <div class="flex flex-col justify-center">
                <h3>Développeur Backend</h3>
                <p class="text-base text-gray-600">
                  Novembre 2017 - Décembre 2018
                </p>
                <div class="text-lg text-gray-600">
                  Lorem ipsum dolor sit amet consectetur adipisicing elit. Qui
                  ab nam animi iure nemo exercitationem a, eius non culpa
                  itaque!
                </div>
              </div>
            </div>
          </li>
          <li>
            <div class="flex">
              <img
                src="~assets/img/carrefour.svg"
                alt="mobile"
                class="h-11 w-11 flex-no-shrink fill-current logo mr-5"
              />
              <div class="flex flex-col justify-center">
                <h3>Testeur et Automaticien</h3>
                <p class="text-base text-gray-600">
                  Septembre 2014 - Novembre 2017
                </p>
                <div class="text-lg text-gray-600">
                  Lorem ipsum dolor sit amet consectetur adipisicing elit. Qui
                  ab nam animi iure nemo exercitationem a, eius non culpa
                  itaque!
                </div>
              </div>
            </div>
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
                  class="h-11 w-11 flex-no-shrink fill-current logo mr-5"
                />
                <div class="flex flex-col justify-center">
                  <h3>{{ project.title }}</h3>
                  <div class="text-lg text-gray-600">
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

        <div
          class="flex flex-col sm:flex-row justify-between items-center mb-16"
        >
          <div>
            <img
              src="~assets/img/avatar.jpg"
              alt="avatar"
              class="w-32 h-32 rounded-full mb-8 lg:mb-0"
            />
          </div>
          <div class="flex-1 text-lg sm:text-xl ml-6">
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Eum quae
            architecto minus molestias iusto ducimus fuga quo quia libero
            dignissimos, fugiat modi assumenda debitis laboriosam.
          </div>
        </div>
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

    return {
      projects,
    };
  },
};
</script>

<style>
</style>
