<template>
  <div>
    <HomeHeroSection />
    <HomeStatSection />
    <div class="max-w-7xl mx-auto mt-14 px-4 sm:px-6 lg:px-8 lg:mt-24">
      <div class="space-y-8 sm:space-y-12">
        <div class="space-y-5 sm:mx-auto sm:max-w-xl sm:space-y-4 lg:max-w-5xl text-center">
          <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">
            Pourquoi cette initiative ?
          </h2>
          <p class="text-xl text-gray-500">
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
          </p>
        </div>
      </div>
      <ProgressBar :voies="voies" class="mt-8 md:mt-10" />
      <Stats :voies="voies" class="mt-8" />
      <Typology :voies="voies" class="mt-8 max-w-2xl mx-auto" />
    </div>
    <div class="max-w-7xl mx-auto mt-14 px-4 sm:px-6 lg:px-8 lg:mt-24">
      <div class="space-y-8 sm:space-y-12">
        <div class="space-y-5 sm:mx-auto sm:max-w-xl sm:space-y-4 lg:max-w-5xl text-center">
          <h2 class="text-3xl font-extrabold tracking-tight sm:text-4xl">
            Avancement par ligne
          </h2>
          <p class="text-xl text-gray-500">
            Choisissez une {{ getRevName('singular') }} pour connaitre le détail du projet et voir son niveau d'avancement.
          </p>
        </div>
        <HomeLinesSection class="mt-5" />
      </div>
    </div>
    <div class="py-16">
      <LvvCta />
    </div>
  </div>
</template>

<script setup>
const { getRevName } = useConfig();

const { data: voies } = await useAsyncData(() => {
  return queryContent('voies-cyclables').where({ _type: 'json' }).find();
});
</script>
