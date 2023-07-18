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
                <button class="prev" @click="prev">Prev</button>
                <button v-if="!isPlaying" class="play" @click="play">Play</button>
                <button v-else class="pause" @click="pause">Pause</button>
                <button class="next" @click="next">Next</button>
            </div>
        </section>
        <section class="playlist">
            <h3>Playlist</h3>
            <button v-for="song in songs" :key="song.src" @click="play(song)"
                    :class="(song.src === current.src) ? 'song playing' : 'song'">{{ song.title }} - {{ song.artist }}
            </button>
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
    methods: {
        play(song) {
            if (typeof song.src != 'undefined') {
                this.current = song
                this.player.src = this.current.src
            }
            this.player.play()
            this.isPlaying = true
        },
        pause() {
            this.player.pause()
            this.isPlaying = false
        },
        next() {
            this.index++
            if (this.index > this.songs.length - 1) {
                this.index = 0
            }
            this.current = this.songs[this.index]
            this.play(this.current)
        },
        prev() {
            this.index--
            if (this.index < 0) {
                this.index = this.songs.length - 1
            }
            this.current = this.songs[this.index]
            this.play(this.current)
        }
    },
    created() {
        this.current = this.songs[this.index]
        this.player.src = this.current.src
    },
}
</script>

<style>
.player {

}

.song-title {
}
</style>
