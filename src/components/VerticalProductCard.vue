<script setup lang="ts">
	import {
		faBars,
		faClockRotateLeft,
		faPen,
		faTrash,
		faTv,
	} from '@fortawesome/free-solid-svg-icons'
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
</script>

<template>
	<div class="vertical-product-card --is-active">
		<div class="vertical-product-card__header">
			<div class="vertical-product-card__header__left-col">
				<div class="vertical-product-card__header__title-label">
					Unit 1 - Page 1 & 2
				</div>
				<div class="vertical-product-card__header__info-label">version 1</div>
			</div>
			<div class="vertical-product-card__header__right-col">
				<div class="vertical-product-card__header__menu-group">
					<button class="vertical-product-card__header__menu-btn">
						<FontAwesomeIcon :icon="faBars" />
					</button>
					<ul class="vertical-product-card__header__menu-list">
						<li class="vertical-product-card__header__menu-item">
							<div class="vertical-product-card__header__menu-item-icon--outer">
								<FontAwesomeIcon
									:icon="faTv"
									class="vertical-product-card__header__menu-item-icon"
								/>
							</div>
							<div class="vertical-product-card__header__menu-item-title">
								View Resources
							</div>
						</li>
						<!-- .vertical-product-card__header__menu-item -->
						<li class="vertical-product-card__header__menu-item">
							<div class="vertical-product-card__header__menu-item-icon--outer">
								<FontAwesomeIcon
									:icon="faPen"
									class="vertical-product-card__header__menu-item-icon"
								/>
							</div>
							<div class="vertical-product-card__header__menu-item-title">
								Edit Resources
							</div>
						</li>
						<!-- .vertical-product-card__header__menu-item -->
						<li class="vertical-product-card__header__menu-item">
							<div class="vertical-product-card__header__menu-item-icon--outer">
								<FontAwesomeIcon
									:icon="faClockRotateLeft"
									class="vertical-product-card__header__menu-item-icon"
								/>
							</div>
							<div class="vertical-product-card__header__menu-item-title">
								Version History
							</div>
						</li>
						<!-- .vertical-product-card__header__menu-item -->
						<li
							class="vertical-product-card__header__menu-item --delete-option"
						>
							<div class="vertical-product-card__header__menu-item-icon--outer">
								<FontAwesomeIcon
									:icon="faTrash"
									class="vertical-product-card__header__menu-item-icon"
								/>
							</div>
							<div class="vertical-product-card__header__menu-item-title">
								Delete Resources
							</div>
						</li>
						<!-- .vertical-product-card__header__menu-item -->
					</ul>
				</div>
			</div>
		</div>
		<div class="vertical-product-card__body">
			<div class="vertical-product-card__body__img--outer">
				<img
					class="vertical-product-card__body__img"
					src="/images/product-image.jpg"
					alt="product image"
				/>
			</div>
		</div>

		<div class="vertical-product-card__footer">
			<div class="vertical-product-card__footer__left-col">
				<button class="vertical-product-card__footer__quick-review-btn">
					<span class="vertical-product-card__footer__quick-review-title">
						Quick review
					</span>
				</button>
			</div>
			<div class="vertical-product-card__footer__right-col">
				<button class="vertical-product-card__footer__play-btn">
					<img
						class="vertical-product-card__footer__play-icon"
						src="/images/icons/play-btn__icon.svg"
						alt="play button"
						width="30"
						height="30"
					/>
					<img
						class="vertical-product-card__footer__play-icon --is-active"
						src="/images/icons/play-btn__icon--active.svg"
						alt="play button"
						width="30"
						height="30"
					/>
				</button>
			</div>
		</div>
	</div>
	<!-- .vertical-product-card -->
</template>

<style lang="scss">
	.vertical-product-card {
		border: 1px solid #cbcbcb;
		border-radius: 15px;
		padding: 14px 18px;
		max-width: 250px;
		flex: 1 1 auto;

		&:hover {
			border-color: $blue-color;
			box-shadow: 2px 2px 20px 0px #3b6ef840;

			.vertical-product-card__footer {
				&__quick-review-btn {
					border-color: $blue-color;
					box-shadow: 2px 2px 10px 0px #00000026;
				}

				&__quick-review-title {
					color: $blue-color;
				}

				&__play-icon {
					display: none;

					&.--is-active {
						display: block;
					}
				}
			}
		}

		@media screen and (min-width: $screen-1200) {
			padding: 20px 24px;
		}

		&__header {
			display: flex;
			justify-content: space-between;

			&__left-col {
				flex: 1 1 auto;
			}

			&__title-label {
				font-size: $font-size-lg;
				font-weight: 600;
				max-width: 100%;
				display: -webkit-box;
				-webkit-box-orient: vertical;
				-webkit-line-clamp: 2;
				overflow: hidden;
				text-overflow: ellipsis;
			}

			&__info-label {
				color: $gray-color-300;
				font-size: 10px;
				font-weight: 300;
				white-space: nowrap;
				max-width: 100%;
				overflow: hidden;
				text-overflow: ellipsis;
			}

			&__right-col {
				min-width: 0;
				flex: 0 0 24px;
				width: 24px;
				margin-left: 8px;
			}

			&__menu-group {
				position: relative;
				width: 24px;
				height: 24px;

				&:hover {
					.vertical-product-card__header {
						&__menu-list {
							display: block;
						}
					}
				}
			}

			&__menu-btn {
				width: 24px;
				height: 24px;
				color: #000;
			}

			&__menu-list {
				display: none;
				position: absolute;
				width: 170px;
				top: 0;
				right: -16px;
				border: 1px solid #cbcbcb;
				box-shadow: 2px 2px 20px 0px #00000040;
				border-radius: 15px;
				padding: 14px;
				z-index: 1;
				background-color: #fff;
			}

			&__menu-item {
				display: flex;
				justify-content: center;
				align-items: center;
				margin-bottom: 4px;
				padding: 2px 5px;
				border-radius: 4px;
				cursor: pointer;

				&:hover {
					background-color: $blue-color;
					color: #fff;

					&.--delete-option {
						background-color: #c92519;
						color: #fff;
					}
				}

				&:last-child {
					margin-bottom: 0;
				}

				&.--delete-option {
					color: #c92519;
				}
			}

			&__menu-item-icon--outer {
				min-width: 0;
				flex: 0 0 18px;
				margin-right: 8px;
			}

			&__menu-item-icon {
				font-size: 12px;
			}

			&__menu-item-title {
				flex: 1 1 auto;
				max-width: 100%;
				display: -webkit-box;
				-webkit-box-orient: vertical;
				-webkit-line-clamp: 2;
				overflow: hidden;
				text-overflow: ellipsis;
				font-size: 12px;
				font-weight: 600;
			}
		}

		&__body {
			&__img--outer {
				position: relative;
				width: 100%;
				padding-bottom: calc(139 / 202) * 100%;
				margin-top: 16px;
				overflow: hidden;
				border-radius: 15px;
			}

			&__img {
				position: absolute;
				top: 0;
				left: 0;
				width: 100%;
				height: 100%;
				object-fit: cover;
			}
		}

		&__footer {
			display: flex;
			align-items: center;
			justify-content: space-between;
			margin-top: 16px;

			&__quick-review-btn {
				padding: 6px 16px;
				border-radius: 8px;
				border: 1px solid #cbcbcb;
			}

			&__right-col {
				display: inline-flex;
				align-items: center;
			}

			&__quick-review-title {
				font-size: 12px;
				white-space: nowrap;
				font-weight: 700;
				color: #172b4d;
			}

			&__play-btn {
				width: 30px;
				height: 30px;
			}

			&__play-icon {
				&.--is-active {
					display: none;
				}
			}
		}
	}
</style>
