<template>
  <div class="bg-white pt-12 sm:pt-16">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="max-w-4xl mx-auto text-center">
        <h2 class="text-3xl font-extrabold text-gray-900 sm:text-4xl">
          Le {{ getRevName() }}, c'est quoi ?
        </h2>
        <p class="mt-3 text-xl text-gray-500 sm:mt-4">
          <strong>B</strong>rest <strong>R</strong>éseau <strong>E</strong>xpress <strong>V</strong>élo, et bref, rapide, quoi.
          <br>Concrètement, une {{ getRevName('singular') }} est une voie cyclable de qualité qui répond à quelques critère simples : sécurisée, directe, bien indiquée et confortable.
          L'ensemble doit créer un maillage cyclable sans discontinuités qui connecte les quartiers brestois aux communes de la périphérie de la métropole.
        </p>
      </div>
    </div>
    <div class="mt-10 bg-white">
      <div class="relative">
        <div class="absolute inset-0 h-1/2 bg-white" />
        <div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div class="max-w-4xl mx-auto">
            <dl class="rounded-lg bg-white shadow-lg sm:grid sm:grid-cols-2">
              <div class="flex flex-col border-b border-gray-100 p-6 text-center sm:border-0 sm:border-r">
                <dt class="order-2 mt-2 text-lg leading-6 font-medium text-gray-500">
                  Lignes<br><small>Linenn</small>
                </dt>
                <dd class="order-1 text-5xl font-extrabold text-lvv-blue-600">
                  10
                </dd>
              </div>
              <div class="flex flex-col border-t border-b border-gray-100 p-6 text-center sm:border-0 sm:border-l sm:border-r">
                <dt class="order-2 mt-2 text-lg leading-6 font-medium text-gray-500">
                  Distance<br><small>Hed</small>
                </dt>
                <dd class="order-1 text-5xl font-extrabold text-lvv-blue-600">
                  140km
                </dd>
              </div>
            </dl>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const { getRevName } = useConfig();
</script>
