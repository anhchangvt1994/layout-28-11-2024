<script lang="ts" setup>
	import { faBell } from '@fortawesome/free-regular-svg-icons'
	import { faChevronDown, faHouse } from '@fortawesome/free-solid-svg-icons'
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

	// NOTE - Notification handler
	const hasNotification = ref<boolean>(true)
	const onClickNotification = () => {
		hasNotification.value = false
	} // onClickNotification
</script>

<template>
	<header class="main-header flex justify-between">
		<div class="main-header__left-col">
			<div class="main-header__page-info text-16">
				<span class="main-header__page-icon">
					<FontAwesomeIcon :icon="faHouse" />
				</span>
				<span class="main-header__page-title text-16 ml-6"
					>Content Management</span
				>
			</div>
		</div>
		<!-- .main-header__left-col -->

		<div
			class="main-header__right-col flex justify-between items-center gap-x-24"
		>
			<div class="main-header__user-info inline-flex items-center">
				<div class="main-header__user-avatar">
					<img
						src="/images/user-avatar.png"
						alt="user avatar"
						width="40"
						height="40"
					/>
				</div>
				<div class="main-header__user-title ml-8">
					<div class="main-header__user-name font-lexend font-bold">
						Jack Kimber
					</div>
					<div
						class="main-header__user-position font-lexend font-medium text-gray-300"
					>
						Content Manager
					</div>
				</div>
				<div class="main-header__user-control ml-8">
					<button class="main-header__user-scale-info">
						<FontAwesomeIcon
							:icon="faChevronDown"
							class="text-10 text-gray-300"
						/>
					</button>
				</div>
			</div>
			<!-- .main-header__user-info -->

			<button
				class="main-header__notification-btn"
				:class="{
					'--is-active': hasNotification,
				}"
				@click="onClickNotification"
			>
				<span class="notification-icon--outer">
					<FontAwesomeIcon
						:icon="faBell"
						class="notification-icon text-white"
					/>
				</span>
			</button>
		</div>
		<!-- .main-header__right-col -->
	</header>
</template>

<style lang="scss">
	.main-header {
		display: flex;
		position: sticky;
		top: 0;
		width: 100%;
		margin-bottom: 8px;
		z-index: 5;
		background-color: $gray-color-100;
		padding: 8px 16px;

		@media screen and (min-width: $screen-1024) {
			margin: 24px 0;
		}

		&__left-col {
			display: none;

			@media screen and (min-width: $screen-1024) {
				display: inline-flex;
				.main-header__page-info {
					display: flex;
					max-width: 300px;
					align-items: center;
				}

				.main-header__page-icon {
					min-width: 0;
					flex: 0 0 18px;
				}

				.main-header__page-title {
					flex: 1 1 auto;
					max-width: 100%;
					white-space: nowrap;
					overflow: hidden;
					text-overflow: ellipsis;
				}
			}
		}

		&__right-col {
			width: 100%;

			@media screen and (min-width: $screen-1024) {
				width: auto;
			}
		}

		&__user-info {
			min-width: 0;
		}

		&__user-avatar {
			width: 40px;
			height: 40px;
			flex: 0 0 40px;
			overflow: hidden;
			border-radius: 50%;

			img {
				width: 100%;
				height: 100%;
				object-fit: cover;
			}
		}

		&__user-title {
			flex: 1 1 0;
			min-width: 0;
		}

		&__user-name {
			font-size: 13px;
			white-space: nowrap;
			overflow: hidden;
			text-overflow: ellipsis;
		}

		&__user-position {
			font-size: 12px;
			white-space: nowrap;
			overflow: hidden;
			text-overflow: ellipsis;
		}

		&__notification-btn {
			display: inline-flex;
			align-items: center;
			justify-content: center;
			border: none;
			background-color: $gray-color-300;
			width: 30px;
			height: 30px;
			flex: 0 0 30px;
			border-radius: 8px;
			min-width: 0;

			.notification-icon--outer {
				position: relative;
				line-height: 1 !important;
			}

			.notification-icon {
				font-size: 15px;
			}

			&.--is-active {
				background-color: $blue-color;

				.notification-icon--outer {
					&:before {
						content: '';
						display: block;
						position: absolute;
						right: 0px;
						top: 0.5px;
						width: 5px;
						height: 5px;
						border-radius: 50%;
						background-color: $red-color;
						border: 1px solid $blue-color;
					}
				}
			}
		}
	}
</style>
