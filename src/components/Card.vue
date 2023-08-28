<script setup>
import { onMounted } from 'vue';
const { character } = defineProps(['character'])
onMounted(() => {
    console.log('Updated Component');
})
</script>
<template>
    <div class="card rnm-card w-96 bg-base-100 shadow-xl border-2 border-white m-5">
        <div class="relative">
            <div class="absolute status-overlay badge"
                :class="character.status == 'Alive' ? 'badge-accent' : 'badge-secondary'">
                <span class="status-text flex items-center">
                    {{ character.status }}
                </span>
            </div>
            <figure>
                <img class="rounded-lg p-2 card-image" :src='character.image' :alt="character.name" />
            </figure>
            <div class="absolute episodes-overlay badge badge-primary">
                <span class="status-text flex items-center">
                    {{ character.episode.length }} Episodes
                </span>
            </div>
        </div>
        <div class="card-body" style="padding: 1rem!important;">
            <div class="w-full flex flex-col">
                <div class="m-0 p-0">
                    <div class="badge badge-primary mr-3">
                        <slot name="species">

                        </slot>
                    </div>
                    <div class="badge badge-accent mr-3">
                        <slot name="gender"></slot>
                    </div>
                </div>
                <div class="m-0 p-0 mt-2">
                    <div class="badge badge-accent">
                        <slot name="origin">

                        </slot>
                    </div>

                </div>
            </div>
            <h2 class="card-title char-name">
                <slot name="name">
                    {{ character.name }}
                </slot>
            </h2>
            <div class="card-actions justify-end">
                <button class="btn btn-primary">View</button>
            </div>
        </div>
    </div>
</template>