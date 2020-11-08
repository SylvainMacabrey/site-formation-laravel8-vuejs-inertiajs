<template>
    <div>
        <div class="bg-gray-200 w-full rounded">
            <div v-if="percentage > 0" class="bg-green-500 text-white text-center rounded-l transition-width duration-500" :style="'width:' + percentage + '%'" >{{ percentage }} %</div>
            <div v-else class="text-white">0 %</div>
        </div>
    </div>
</template>

<script>
export default {

    props: ['watchedEpisodes', 'episodes'],

    data() {
        return {
            watchedEpisodesData: this.watchedEpisodes
        }
    },

    computed: {
        percentage() {
            let filteredEp = this.episodes.filter(courseEp => {
                return this.watchedEpisodesData.find(watchedEp => {
                    return watchedEp.id == courseEp.id
                })
            })
            return Math.round((filteredEp.length/this.episodes.length)*100)
        }
    },

    mounted() {
        eventBus.$on('toggleProgress', data => this.watchedEpisodesData = data)
    }

}
</script>
