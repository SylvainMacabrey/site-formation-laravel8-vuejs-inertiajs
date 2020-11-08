<template>
    <app-layout>
        <template #header>Formations</template>
        <div class="bg-green-200 text-green-500 p-3" v-if="$page.flash.success">{{ $page.flash.success }}</div>
        <div class="py-6" v-for="course in this.courseList.data" v-bind:key="course.id">
            <div class="mx-8 bg-white rounded shadow p-4">
                <div class="text-sm text-gray-500">Mis en ligne par {{ course.user.name }} - <span>{{ course.participants }}</span> participant<span v-if="parseInt(course.participants) > 1">s</span> - {{ course.episodes_count }} épisodes</div>
                <div class="flex justify-between items-center">
                    <div class="text-4xl">{{ course.title }}</div>
                </div>
                <div class="text-sm text-gray-500">{{ course.description }}</div>
                <div class="flex items-center justify-between">
                    <div></div>
                    <div>
                        <a :href="route('courses.edit', course.id)" v-if="course.update" class="bg-blue-500 text-white px-2 py-1 text-sm mt-3 rounded hover:bg-blue-700 inline-block">Modifier la formation</a>
                        <a :href="route('courses.show', course.id)" class="bg-indigo-500 text-white px-2 py-1 text-sm mt-3 rounded hover:bg-indigo-700 inline-block">Voir la formation</a>
                    </div>
                </div>
            </div>
        </div>
        <div class="text-center">
            <inertia-link class="text-indigo-700 border-gray-500 p-5" :href="link.url" v-for="link in courses.links" v-bind:key="link.label">
                <button :class="{'text-white bg-indigo-700 py-2 px-5' : link.active}">{{ link.label }}</button>
            </inertia-link>
        </div>
    </app-layout>
</template>

<script>
import AppLayout from './../../Layouts/AppLayout'

export default {

    components: {
        AppLayout
    },

    props: ['courses'],

    data() {
        return {
            courseList: this.courses
        }
    },

}
</script>
