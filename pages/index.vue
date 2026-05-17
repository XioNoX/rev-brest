<template>
  <div>
    <HomeHeroSection />
    <HomeStatSection />
    <div class="max-w-7xl mx-auto mt-14 px-4 sm:px-6 lg:px-8 lg:mt-24">
      <div class="space-y-8 sm:space-y-12">
        <div class="space-y-5 sm:mx-auto sm:max-w-xl sm:space-y-4 lg:max-w-5xl text-center">
          <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">Pourquoi cette initiative ?</h2>
            <ul class="text-xl text-gray-500">
              <li>
               Pour que les cyclistes de Brest puissent se déplacer en sécurité sur leurs trajets quotidiens.
              </li>
              <li>
                Pour que les aménagements à venir sur les lignes définies ici prennent en compte le cahier des charges des <u><a href=/blog/reseau-express-velo>REV</a></u>.
              </li>
              <li>
                Pour que les habitant.e.s de la Métropole puissent se déplacer sans voiture et le coût qui lui est associé.
              </li>
              <li>
                Pour donner des idées aux élu.e.s en cours et futurs. Maintenant que le projet du 2ème tram est sur des rails.
              </li>
              <li>
                Pour que Brest Métropole se mette à la page des autres métropoles d'envergure.
              </li>
            </ul>
        </div>
      </div>
      <ProgressBar :voies="voies" class="mt-8 md:mt-10" />
      <Stats :voies="voies" class="mt-8" />
      <StatsQuality v-if="displayQuality() && displayQualityOnHomePage()" :voies="voies" class="mt-8" />
      <Typology :voies="voies" class="mt-8 max-w-2xl mx-auto" />
    </div>
    <div>
      <NuxtLink href="/tableau-de-bord" class="flex items-center justify-center text-lvv-blue-600 hover:underline">
        Voir le tableau de bord complet
        <Icon name="heroicons:arrow-right" class="ml-1 h-5 w-5" />
      </NuxtLink>
    </div>
    <div class="max-w-7xl mx-auto mt-14 px-4 sm:px-6 lg:px-8 lg:mt-24">
      <div class="space-y-8 sm:space-y-12">
        <div class="space-y-5 sm:mx-auto sm:max-w-xl sm:space-y-4 lg:max-w-5xl text-center">
          <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">Avancement par ligne</h2>
          <p class="text-xl text-gray-500">
            Choisissez une {{ getRevName('singular') }} pour connaitre le détail du projet et voir son niveau
            d'avancement.
          </p>
        </div>
        <HomeLinesSection class="mt-5" />
      </div>
    </div>

    <div v-if="displayCounters()" class="max-w-7xl mx-auto mt-14 px-4 sm:px-6 lg:px-8 lg:mt-24">
      <div class="space-y-5 sm:mx-auto sm:max-w-xl sm:space-y-4 lg:max-w-5xl text-center">
        <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">Compteurs de passages</h2>
        <p class="text-xl text-gray-500">
          Suivez l'évolution de la fréquentation cycliste grâce aux {{ counterCount }} compteurs de Brest métropole.
        </p>
      </div>
      <div class="mt-8 flex flex-wrap justify-center gap-4">
        <NuxtLink
          to="/compteurs/velo"
          class="flex items-center gap-4 p-4 rounded-lg border border-gray-200 hover:border-lvv-blue-600 hover:shadow-md transition-all group w-full sm:w-auto sm:min-w-[250px]"
        >
          <div class="flex-shrink-0 w-12 h-12 rounded-full bg-pink-100 flex items-center justify-center">
            <Icon name="game-icons:dutch-bike" class="text-2xl text-pink-600" />
          </div>
          <div>
            <div class="font-semibold text-gray-900 group-hover:text-lvv-blue-600">Compteurs vélo</div>
            <div class="text-sm text-gray-500">Fréquentation cycliste</div>
          </div>
        </NuxtLink>
      </div>
    </div>
    <div class="py-16">
      <LvvCta />
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Collections } from '@nuxt/content';

const { getRevName, displayQuality, displayQualityOnHomePage, displayCounters } = useConfig();

const { geojsons } = await useVoiesCyclablesGeojson();
const voies: Ref<Collections['voiesCyclablesGeojson'][]> = computed(() => geojsons.value || []);

const { data: counterData } = await useAsyncData(
  'home-counter-count',
  () => {
    if (!displayCounters()) return Promise.resolve(null);
    return queryCollection('compteurs').where('path', 'LIKE', '/compteurs/velo%').all();
  },
  { deep: false },
);
const counterCount = computed(() => counterData.value?.length ?? 0);
</script>
