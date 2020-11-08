<template>
    <app-layout>
        <template #header>{{ courseShow.title }}</template>
        <div class="py-6">
            <div class="mx-8 bg-white rounded shadow p-4">
                <div class="text-sm text-gray-500">Mis en ligne par {{ courseShow.user.name }}</div>
                <div class="flex justify-between items-center">
                    <div class="text-4xl">{{ courseShow.title }}</div>
                    <div class="text-sm text-gray-500">{{ courseShow.episodes_count }} épisodes</div>
                </div>
                <div class="text-sm text-gray-500">{{ courseShow.description }}</div>
            </div>
        </div>
        <div class="py-4">
            <div class="mx-8 bg-white rounded shadow p-4">
                <div class="text-2xl">Chapitre {{ currentKey + 1 }} : {{ courseShow.episodes[this.currentKey].title }}</div>
                <div class="text-sm text-gray-500">{{ courseShow.episodes[this.currentKey].description }}</div>
                <iframe class="w-full h-screen" :src="courseShow.episodes[this.currentKey].video_url" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
            </div>
        </div>
        <div class="py-4">
            <div class="mx-8 bg-white rounded shadow p-4">
                <div class="py-6">
                    <progress-bar :watchedEpisodes="watched" :episodes="courseShow.episodes"/>
                </div>
                <ul v-for="(episode, index) in this.courseShow.episodes" v-bind:key="episode.id">
                    <li class="mt-3 flex justify-between items-center">
                        <div>
                            Chapitre {{ index + 1 }} - {{ episode.title }}
                            <button class="text-gray-500 focus:text-indigo-500 hover:text-indigo-700" @click="switchEpisode(index)">Voir épisode</button>
                        </div>
                        <progress-button :episodeId="episode.id" :watchedEpisodes="watched"/>
                    </li>
                </ul>
            </div>
        </div>
    </app-layout>
</template>

<script>
import AppLayout from './../../Layouts/AppLayout'
import ProgressButton from './ProgressButton'
import ProgressBar from './ProgressBar'

export default {

    components: {
        AppLayout,
        ProgressButton,
        ProgressBar
    },

    props: ['course', 'watched'],

    data() {
        console.log(this.watched)
        return {
            courseShow: this.course,
            currentKey: 0
        }
    },

    methods: {
        switchEpisode(index) {
            this.currentKey = index
            window.scrollTo({
                top: 0,
                left: 0,
                behavior: 'smooth'
            })
        }
    },

}
</script>
