<template lang="pug">
    section(class="section")
        div(class="columns")
            div(class="column is-4")
                div(class="card")
                    div(class="card-content")
                        div(class="card-carousel" @mouseover="stopTimer" @mouseleave="restartTimer")
                            div(class="progressbar" v-if="autoSlideInterval && showProgressBar")
                                div(:style="{width: progressBar + '%'}")
                            div(class="card-img")
                                img(:src="images[activeImage].big" alt="")
                                div(class="actions")
                                    span(@click="prevImage" class="prev")
                                        | &#8249;
                                    span(class="next" @click="nextImage")
                                        | &#8250;
                            div(class="thumbnails")
                                div(v-for="(image, index) in images" :key="image.id" :class="['thumbnail-img', (activeImage === index)?'active':'']" @click="activateImage(index)")
                                    img(:src="image.thumb" alt="")
</template>

<script>
export default {
    data: function() {
        return {
            activeImage: 0,
            autoSlideTimeout: null,
            stopSlider: false,
            timeLeft: 0,
            timerInterval: null,
            countdownInterval: 4000,
            autoSlideInterval: 5000
        }
    },
    computed: {
        currentImage: function() {
            this.timeLeft = this.autoSlideInterval
            return this.images[activeImage].big
        },
        progressBar: function() {
            return 100 - (this.timeLeft/this.autoSlideInterval) * 100
        }
    },
    methods: {
        nextImage: function() {
            var active = this.activeImage + 1
            if(active >= this.images.length) {
                active = 0
            }
            this.activateImage(active)
        },
        prevImage: function() {
            var activr = this.activeImage - 1
            if(active < 0) {
                active = this.images.length - 1
            }
            this.activateImage(active)
        },
        activateImage: function(imageIndex) {
            this.activeImage = imageIndex
        },
        startTimer: function(interval) {
            if(interval && interval > 0 && !this.stopSlider) {
                var self = this
                clearTimeout(this.autoSlideTimeout)
                this.autoSlideTimeout = setTimeout(function() {
                    self.nextImage()
                    self.startTimer(self.autoSlideInterval)
                }, interval)
            }
        },
        stopTimer: function() {
            clearTimeout(this.autoSlideTimeout)
            this.stopTimer = true
            clearInterval(this.timerInterval)
        },
        restartTimer: function() {
            this.stopSlider = false
            clearInterval(this.timerInterval)
            this.startCountdown()
            this.startTimer(this.timeLeft)
        },
        startCountdown: function() {
            if(!this.showProgressBar) return
            var self = this
            this.timerInterval = setInterval(() => {
                self.timeLeft -= self.countdownInterval
                if(self.timeLeft <= 0) {
                    self.timeLeft = self.autoSlideInterval
                }
            }, this.countdownInterval);
        }
    },
    created: function() {
        if(this.startingImage 
            && this.startingImage >= 0
            && this.startingImage < this.images.length) {
            this.activeImage = this.startingImage;
        }
        if(this.autoSlideInterval
            && this.autoSlideInterval > this.countdownInterval) {
            this.startTimer(this.autoSlideInterval);
            this.timeLeft = this.autoSlideInterval;
            this.startCountdown();
        }
    },
    props: ['startingImage', 'images', 'showProgressBar']
}
</script>

<style scoped>
.card-carousel {
    user-select: none;
    position: relative;
}
.progressbar {
    display: block;
    width: 100%;
    height: 5px;
    position: absolute;
    background-color: rgba(61, 43, 43, 0.25);
    z-index: 1;
}
.progressbar > div {
    background-color: rgba(255, 255, 255, 0.52);
    height: 100%;
}
.thumbnails {
    display:flex;
    justify-content: space-evenly;
    flex-direction: row;
}
.thumbnail-img {
    display: flex;
    align-items: center;
    cursor: pointer;
    padding: 20px;
}
.thumbnail-img > img {
    width: 100%;
    height: auto;
    transition: all 250ms;
}
.thumbnail-img:hover > img,
.thumbnail-img:active > img {
    opacity: 0.6;
    box-shadow: 2px 2px 6px 1px rgba(0,0,0,0.5); 
}
.card-img {
    position: relative;
    margin-bottom: 15px;
}
.card-img > img {
    display: block;
    margin: 0 auto;
}
.actions {
    font-size: 1.5em;
    height: 40px;
    position: absolute;
    top: 50%;
    margin-top: -20px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #585858;
}
.actions > span {
    cursor: pointer;
    transition: all 250ms;
    font-size: 45px;
}
.actions > span.prev {
    margin-left: 5px;
}
.actions > span.next {
    margin-right: 5px;
}
.actions > span:hover {
    color: #eee;
}
.active {
    color: #eee;
}
</style>