<template>
	<div>
		<button @click="$emit('prev')" class="carousel-controls left">Prev</button>
		<button @click="$emit('next')" class="carousel-controls right">Next</button>
	</div>
</template>

<script>
	export default {
		emits: ['prev', 'next']
	}
</script>

<style lang="scss" scoped>
	.carousel-controls {
		border: none;
		background: rgba(0, 0, 0, .5);
		position: absolute;
		height: 50px;
		width: 70px;
		top: 50%;
		transform: translateY(-50%);
		color: #f3f3f3;
		cursor: pointer;
		transition: .5s;

		&:hover {
			background: rgba(0, 0, 0, .8);
		}

		&.left {
			left: 0;
		}

		&.right {
			right: 0;
		}
	}
</style>