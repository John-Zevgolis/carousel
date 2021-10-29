<template>
	<div class="carousel">
	    <div class="carousel-inner" :style="dimention">
	      <carousel-indicators v-if="indicators" :count="slides.length" :active="currentSlide" @switch="switchSlide($event)"></carousel-indicators>
	      <carousel-item v-for="(slide, index) in slides" :key="`slide-${index}`" :index="index" :currentSlide="currentSlide" :slide="slide" :direction="direction" @mouseenter="stopSlideTimer" @mouseout="startSlideTimer"></carousel-item>
	      <carousel-controls v-if="controls" @prev="prev" @next="next"></carousel-controls>
	    </div>
	</div>
</template>

<script>
	import CarouselItem from './CarouselItem.vue';
	import CarouselControls from './CarouselControls.vue';
	import CarouselIndicators from './CarouselIndicators.vue';

	export default {
		props: {
			slides: {
				type: Array,
				required: true
			},
			controls: {
				type: Boolean,
				default: false
			},
			indicators: {
				type: Boolean,
				default: false
			},
			interval: {
				type: Number,
				default: 5000
			},
			width: {
				type: Number,
				default: 900
			},
			height: {
				type: Number,
				default: 400
			}
		},
		components: {
			CarouselItem,
			CarouselControls,
			CarouselIndicators
		},
		data() {
			return {
				currentSlide: 0,
				slideInterval: null,
				direction: 'right'
			}
		},
		beforeUnmount() {
			this.stopSlideTimer();
		},
		mounted() {
			this.startSlideTimer();
		},
		methods: {
			setCurrentSlide(index) {
				this.currentSlide = index;
			},
			prev(step = -1) {
				const index = this.currentSlide > 0 ? this.currentSlide + step : this.slides.length - 1;
				this.setCurrentSlide(index);
				this.direction = 'left';
				this.startSlideTimer();
			},
			_next(step = 1) {
				const index = this.currentSlide < this.slides.length - 1 ? this.currentSlide + step : 0;
				this.setCurrentSlide(index);
				this.direction = 'right';
			},
			next(step = 1) {
				this._next(step);
				this.startSlideTimer();
			},
			startSlideTimer() {
				this.stopSlideTimer();
				this.slideInterval = setInterval(() => {
					this._next();
				}, this.interval);
			},
			stopSlideTimer() {
				clearInterval(this.slideInterval);
			},
			switchSlide(index) {
				const step = index - this.currentSlide;
				if(step > 0) {
					this.next(step);
				} else {
					this.prev(step);
				}
			}
		},
		computed: {
			dimention() {
				return {
					width: this.width + 'px',
					height: this.height + 'px'
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.carousel {
		display: flex;
		justify-content: center;

		.carousel-inner {
			position: relative;
			overflow: hidden;
		}
	}
</style>