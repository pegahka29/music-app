<template>
    <div id="app">
        <header>
            <h1>My Music </h1>
        </header>
        <section class="player">
            <h2 class="song-title">{{ current.title }} -<span>
                {{ current.artist }}
            </span>
            </h2>
            <div class="controls">
                <button class="prev">Prev</button>
                <button v-if="!isPlaying" class="play">Play</button>
                <button v-else class="pause">Pause</button>
                <button class="next">Next</button>
            </div>
        </section>
    </div>
</template>

<script>

export default {
    name: 'App',
    components: {},
    data() {
        return {
            index: 0,
            current: {},
            isPlaying: false,
            songs: [
                {
                    title: 'Tab',
                    artist: 'ariyan band',
                    src: require('./assets/Tab.mp3')
                },
                {
                    title: 'Lahzeha',
                    artist: 'ariyan band',
                    src: require('./assets/Lahzeha.mp3')
                },
                {
                    title: 'Ki be joz man',
                    artist: 'ariyan band',
                    src: require('./assets/KiBeJozMan.mp3')
                },
                {
                    title: 'Hanoz baram hamoni',
                    artist: 'ariyan band',
                    src: require('./assets/HanozBaramHamoni.mp3')
                },
                {
                    title: 'Bi to ba to',
                    artist: 'ariyan band',
                    src: require('./assets/BiToBaTo.mp3')
                },
            ],
            player: new Audio()
        }
    },
    created() {
        this.current = this.songs[this.index]
        this.player.src = this.current.src
        // this.player.play()
    },
}
</script>

<style>
.player {

}

.song-title {
}
</style>
