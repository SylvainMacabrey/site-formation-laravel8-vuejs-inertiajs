<template>
    <app-layout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Dashboard
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-green-200 text-green-500 p-3" v-if="$page.flash.success">{{ $page.flash.success }}</div>
                <div class="w-full">
                    <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="submit">
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-bold mb-2" for="title">Titre de la formation</label>
                            <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="title" type="text" v-model="form.title">
                            <div class="bg-red-200 text-red-800 p-4 my-2" v-if="$page.errors.title">{{ $page.errors.title }}</div>
                        </div>
                        <div class="mb-4">
                            <label class="block text-gray-700 text-sm font-bold mb-2" for="description">Description de la formation</label>
                            <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="description" type="text" v-model="form.description"></textarea>
                            <div class="bg-red-200 text-red-800 p-4 my-2" v-if="$page.errors.description">{{ $page.errors.description }}</div>
                        </div>
                        <div class="mb-4">
                            <h2 class="text-2xl">Episode(s) de la formation</h2>
                            <div class="mb-10" v-for="(episode, index) in form.episodes" v-bind:key="index">
                                <label class="block text-gray-700 text-sm font-bold mb-2" :for="'title-'+index">Titre de l'épisode n°{{ index + 1 }} </label>
                                <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" :id="'title-'+index" type="text" v-model="form.episodes[index].title">
                                <div class="bg-red-200 text-red-800 p-4 my-2" v-if="$page.errors['episodes.'+index+'.title']">{{ $page.errors['episodes.'+index+'.title'] }}</div>
                                <label class="block text-gray-700 text-sm font-bold mb-2" :for="'description-'+index">Description de l'épisode n°{{ index + 1 }} </label>
                                <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" :id="'description-'+index" type="text" v-model="form.episodes[index].description"></textarea>
                                <div class="bg-red-200 text-red-800 p-4 my-2" v-if="$page.errors['episodes.'+index+'.description']">{{ $page.errors['episodes.'+index+'.description'] }}</div>
                                <label class="block text-gray-700 text-sm font-bold mb-2" :for="'video_url-'+index">URL de la vidéo</label>
                                <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" :id="'video_url-'+index" type="text" v-model="form.episodes[index].video_url">
                                <div class="bg-red-200 text-red-800 p-4 my-2" v-if="$page.errors['episodes.'+index+'.video_url']">{{ $page.errors['episodes.'+index+'.video_url'] }}</div>

                            </div>
                        </div>
                        <div class="flex items-center justify-between">
                            <div class="flex">
                                <button class="bg-green-600 py-2 px-4 rounded mx-2 text-white block" v-if="form.episodes.length < 15" @click.prevent="add">+</button>
                                <button class="bg-red-600 py-2 px-4 rounded mx-2 text-white block" v-if="form.episodes.length > 1" @click.prevent="remove">-</button>
                            </div>
                            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                                Créer la formation
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>

    </app-layout>
</template>

<script>
import AppLayout from '@/Layouts/AppLayout'

export default {

    components: {
        AppLayout,
    },

    data() {
        return {
            form: {
                title: null,
                description:  null,
                episodes: [
                    {
                        title: null,
                        desccription: null,
                        video_url: null
                    }
                ]
            }
        }
    },

    methods: {
        submit() {
            this.$inertia.post('/courses', this.form)
            this.form = {
                title: null,
                description:  null,
                episodes: [
                    {
                        title: null,
                        desccription: null,
                        video_url: null
                    }
                ]
            }
        },
        add() {
            this.form.episodes.push({
                title: null,
                desccription: null,
                video_url: null
            })
        },
        remove() {
            this.form.episodes.pop()
        }
    },

}
</script>
