<script lang="ts" setup>
	import { faArrowDownAZ } from '@fortawesome/free-solid-svg-icons'
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
</script>

<template>
	<div class="filter-bar flex items-center">
		<label
			for="filter-bar-select"
			class="filter-bar__left-col inline-flex items-center mr-12"
		>
			<span class="filter-bar__icon--outer">
				<FontAwesomeIcon :icon="faArrowDownAZ" class="filter-bar__icon" />
			</span>
			<div class="filter-bar__title">Sort</div>
		</label>
		<div class="filter-bar__right-col">
			<select id="filter-bar-select" class="filter-bar__select" name="">
				<option class="filter-bar__option">NEWEST</option>
				<option class="filter-bar__option">OLDEST</option>
				<option class="filter-bar__option">TRENDING</option>
			</select>
		</div>
	</div>
	<!-- .filter-bar -->
</template>

<style lang="scss">
	.filter-bar {
		&__icon--outer {
			display: inline-flex;
		}

		&__icon {
			font-size: $font-size-lg;
			color: #828282;
		}
		&__title {
			font-size: $font-size-lg;
			margin-left: 8px;
			color: #828282;
		}
		&__select {
			height: 32px;
			width: 100%;
			padding: 0 8px;
			font-size: 13px;
			background-color: #fff;
			height: 32px;
			border: 1px solid #d6d6d6;
			border-radius: 4px;

			@media screen and (min-width: $screen-1024) {
				height: 40px;
			}
		}
	}
</style>
