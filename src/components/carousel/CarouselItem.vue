<template>
	<transition :name="transitionName">
		<div class="carousel-item" v-show="currentSlide === index" @mouseenter="$emit('mouseenter')" @mouseout="$emit('mouseout')">
	        <img :src="slide">
	    </div>
	 </transition>
 </template>

 <script>
 	export default {
 		emits: ['mouseenter', 'mouseout'],
 		props: ['slide', 'currentSlide', 'index', 'direction'],
 		computed: {
 			transitionName() {
 				return this.direction === 'right' ? 'slide-out' : 'slide-in';
 			}
 		}
 	}
 </script>

 <style lang="scss" scoped>
	.carousel-item {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
	}

	.slide-out-enter-active,
	.slide-out-leave-active,
	.slide-in-enter-active,
	.slide-in-leave-active  {
		transition: all 1s ease-in-out;
	}

	.slide-out-enter-from {
		transform: translateX(100%);
	}

	.slide-out-leave-to {
		transform: translateX(-100%);
	}

	.slide-in-enter-from {
		transform: translateX(-100%);
	}

	.slide-in-leave-to {
		transform: translateX(100%);
	}
</style>