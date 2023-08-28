<script setup>
import Card from "./Card.vue"
import axios from "axios"
import { ref, watch, onMounted } from "vue";
const baseURL = "https://rickandmortyapi.com/api"


const nextPageURL = ref('')
const previousPageURL = ref('')

const characters = ref(null)
const page = ref(1)


watch(page, async () => {
    const res = await axios.get(baseURL + "/character?page=" + page.value)
    updatePageData(res)
})

onMounted(async () => {
    const response = await axios.get(baseURL + "/character")
    updatePageData(response)
})

function updatePageData(response) {
    characters.value = response.data.results;
    nextPageURL.value = response.data.info.next
    previousPageURL.value = response.data.info.previous ? response.data.info.previous : ''
}

</script>

<template>
    <div class="h-12 w-full px-12 py-10 flex items-center justify-between">
        <button class="btn btn-accent" @click="if (page > 1) page--;">
            Previous
        </button>
        <div class="prose text-center">
            <button @click="page = 1" class="no-underline">
                <h1 class="mb-0">
                    Rick & Morty
                </h1>
            </button>
            <h3 class="mt-0">
                Page {{ page }}
            </h3>
        </div>
        <button class="btn btn-accent" @click="if (page < 42) page++;">
            Next
        </button>
    </div>
    <div class="w-full px-2 pb-12">
        <div>
            <ul>
                <TransitionGroup class="flex flex-row flex-wrap mx-auto items-center justify-center" name="list" tag="ul">
                    <li v-for="(character, index) in characters" :key="index">
                        <Card :character="character">
                            <template #species>
                                {{ character.species }}
                            </template>
                            <template #gender>
                                {{ character.gender }}
                            </template>
                            <template #origin>
                                {{ character.origin.name }}
                            </template>
                            <template #name>
                                {{ character.name }}
                            </template>
                        </Card>
                    </li>
                </TransitionGroup>
            </ul>
        </div>
    </div>
</template> 

<style scoped>
.list-enter-active,
.list-leave-active {
    transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
    opacity: 0;
    transform: translateY(-50px);
}
</style>