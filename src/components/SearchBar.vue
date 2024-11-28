<script lang="ts" setup>
	import { faMagnifyingGlass } from '@fortawesome/free-solid-svg-icons'
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
</script>

<template>
	<div class="search-bar">
		<input
			id="search-bar-input"
			class="search-bar__input"
			type="text"
			placeholder="Search Resources"
		/>
		<label for="search-bar-input" class="search-bar__icon--outer">
			<FontAwesomeIcon :icon="faMagnifyingGlass" class="search-bar__icon" />
		</label>
	</div>
	<!-- .search-bar -->
</template>

<style lang="scss">
	.search-bar {
		display: flex;
		position: relative;
		height: 32px;
		z-index: 0;

		@media screen and (min-width: $screen-1024) {
			height: 40px;
		}

		&__icon--outer {
			position: absolute;
			left: 0;
			top: 0;
			display: inline-flex;
			align-items: center;
			height: 100%;
			min-width: 0;
			padding-left: 16px;
			padding-right: 12px;
			border-top-left-radius: 4px;
			border-bottom-left-radius: 4px;
		}

		&__icon {
			font-size: $font-size-md;
			color: $gray-color-400;
		}

		&__input {
			position: absolute;
			left: 0;
			left: 0;
			z-index: -1;
			height: 100%;
			width: 100%;
			padding-left: 40px;
			padding-right: 8px;
			font-size: 13px;
			background-color: #fff;
			height: 32px;
			border: 1px solid #d6d6d6;
			border-radius: 4px;

			@media screen and (min-width: $screen-1024) {
				height: 40px;
			}

			&::placeholder {
				color: #828282;
			}

			&:focus {
				border-radius: 8px;
				border-color: #2563eb;
				font-family: 'Poppins', 'sans-serif';

				&::placeholder {
					color: $blue-color;
					font-weight: 700;
				}

				& + .search-bar__icon--outer {
					border-top-left-radius: 8px;
					border-bottom-left-radius: 8px;

					.search-bar__icon {
						color: $blue-color;
					}
				}
			}
		}
	}
</style>
