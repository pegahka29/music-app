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
                <button v-else class="play" @click="pause">Pause</button>
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
            this.player.addEventListener('ended', function () {
                this.index++
                if (this.index > this.songs.length - 1) {
                    this.index = 0
                }
                this.current = this.songs[this.index]
                this.play(this.current)
            }.bind(this))
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
main {
    width: 100%;
    max-width: 768px;
    margin: 0 auto;
    padding: 25px;
}

button {
    appearance: none;
    background: none;
    border: none;
    outline: none;
    cursor: pointer;
}

button:hover {
    opacity: 0.8;
}

.play {
    font-size: 20px;
    font-weight: 700;
    padding: 15px 25px;
    border-radius: 8px;
    color: #FFF;
    background: #CC2E5D;
}

.song-title {
    color: #53565a;
    font-size: 32px;
    font-weight: 700;
    text-transform: uppercase;
    text-align: center;
}

.song-title span {
    font-weight: 400;
    font-style: italic;
}

.controls {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 30px 15px;
}

.next, .prev {
    font-size: 16px;
    font-weight: 700;
    padding: 10px 15px;
    margin: 0 15px;
    border-radius: 6px;
    color: #FFF;
    background: #FF5858;
}

.playlist {
    padding: 0 30px;
}

.playlist h3 {
    color: #212121;
    font-size: 28px;
    font-weight: 400;
    margin-bottom: 30px;
    text-align: center;
}

.playlist .song {
    display: block;
    width: 100%;
    padding: 15px;
    font-size: 20px;
    font-weight: 700;
    cursor: pointer;
}

.playlist .song:hover {
    color: #FF5858;
}

.playlist .song.playing {
    color: #FFFFFF;
    background: linear-gradient(to right, #CC2E5D, #FF5858);
}
</style>
