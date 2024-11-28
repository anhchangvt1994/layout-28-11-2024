<script setup lang="ts">
	import { faBoxArchive } from '@fortawesome/free-solid-svg-icons'
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
	import SearchBar from 'components/SearchBar.vue'
	import SearchTagBar from 'components/SearchTagBar.vue'
	import VerticalProductCard from 'components/VerticalProductCard.vue'
	import FilterBar from 'components/FilterBar.vue'
	import BreakPageButton from 'components/home-page/BreakPageButton.vue'
</script>

<template>
	<section class="home-page">
		<div class="home-page__header">
			<div class="home-page__header__left-col">
				<div class="home-page__header__title-label">CONTENT MANAGEMENT</div>
			</div>
			<div class="home-page__header__right-col">
				<button class="home-page__header__upload-btn">
					<div class="home-page__header__upload-icon--outer">
						<FontAwesomeIcon
							:icon="faBoxArchive"
							class="home-page__header__upload-icon"
						/>
					</div>
					<div class="home-page__header__upload-title">NEW UPLOAD</div>
				</button>
			</div>
		</div>
		<!-- .header -->
		<div class="home-page__body">
			<div class="home-page__body__body-inner">
				<div class="home-page__body__interactive-block flex flex-wrap gap-8">
					<SearchBar class="home-page__search-bar flex-[1_1_100%] 480:flex-1" />
					<SearchTagBar
						class="home-page__search-tag-bar 480:flex-1 flex-[1_1_100%]"
					/>
					<FilterBar />
				</div>

				<div class="home-page__body__content-block">
					<div class="home-page__body__content-block--inner">
						<VerticalProductCard v-for="i in 8" :key="i" />
					</div>
				</div>

				<div class="home-page__body__footer pt-20 pb-10">
					<BreakPageButton :total="3" />
				</div>
			</div>
		</div>
		<!-- .body -->
	</section>
	<!-- .home-page -->
</template>

<style lang="scss">
	.home-page {
		&__header {
			display: flex;
			align-items: center;
			font-size: $font-size-lg;
			font-weight: 500;
			padding-top: 8px;
			padding-bottom: 16px;
			justify-content: space-between;

			&__title-label {
				display: -webkit-box;
				-webkit-box-orient: vertical;
				-webkit-line-clamp: 3;
				overflow: hidden;
				text-overflow: ellipsis;
			}

			&__upload-btn {
				display: none;
				align-items: center;
				background-color: $blue-color;
				border-radius: 6px;
				color: #fff;
				padding: 12px 24px;
			}

			&__upload-icon--outer {
				display: inline-flex;
				margin-right: 10px;
			}

			&__upload-icon {
				font-size: $font-size-lg;
				color: #fff;
			}

			&__upload-title {
				font-size: 13px;
				font-weight: 700;
			}

			@media screen and (min-width: $screen-1024) {
				&__upload-btn {
					display: flex;
				}
			}
		}

		&__body {
			&__inner {
				max-width: 508px;
				margin: 0 auto;

				@media screen and (min-width: $screen-768) {
					max-width: 768px;
				}

				@media screen and (min-width: $screen-992) {
					max-width: 992px;
				}

				@media screen and (min-width: $screen-1024) {
					max-width: 800px;
				}

				@media screen and (min-width: $screen-1200) {
					max-width: 888px;
				}

				@media screen and (min-width: $screen-1366) {
					max-width: none;
				}
			}

			&__interactive-block {
				margin-bottom: 20px;
				justify-content: center;
			}

			&__content-block {
				display: flex;
				justify-content: center;

				&--inner {
					display: flex;
					flex-wrap: wrap;
					justify-content: center;
					gap: 8px;

					@media screen and (min-width: $screen-520) {
						justify-content: start;
						.vertical-product-card {
							max-width: none;
							flex: 0 0 calc(1 / 2 * 100% - 4px);
						}
					}

					@media screen and (min-width: $screen-768) {
						.vertical-product-card {
							flex: 0 0 calc(1 / 3 * 100% - 6px);
						}
					}

					@media screen and (min-width: $screen-992) {
						.vertical-product-card {
							flex: 0 0 calc(1 / 4 * 100% - 6px);
						}
					}

					@media screen and (min-width: $screen-1024) {
						gap: 20px 8px;

						.vertical-product-card {
							flex: 0 0 calc(1 / 3 * 100% - 6px);
						}
					}

					@media screen and (min-width: $screen-1200) {
						gap: 20px;

						.vertical-product-card {
							flex: 0 0 calc(1 / 3 * 100% - 14px);
						}
					}

					@media screen and (min-width: $screen-1366) {
						gap: 20px;

						.vertical-product-card {
							flex: 0 0 calc(1 / 4 * 100% - 15px);
						}
					}
				}
			}

			&__footer {
				display: flex;
				justify-content: center;

				@media screen and (min-width: $screen-1024) {
					justify-content: end;
				}
			}
		}

		.filter-bar {
			display: none;
		}

		@media screen and (min-width: $screen-1024) {
			.filter-bar {
				display: inline-flex;
				margin-left: auto;
				padding-left: 16px;
			}

			.search-bar,
			.search-tag-bar {
				max-width: 345px;
			}
		}
	}
</style>
