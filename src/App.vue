<script setup>
import RickAndMortyCard from './components/RickAndMortyCard.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      <Suspense>
        <template #default>
          <RickAndMortyCard />
        </template>
        <template #fallback>
          <div class="prose">
            <div class="flex flex-row item-center justify-center">
              <h1>
                Loading...
              </h1>
            </div>
          </div>
        </template>
      </Suspense>
    </div>
  </header>

  <main>

  </main>
</template>

<style scoped></style>
