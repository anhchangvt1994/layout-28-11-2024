<script lang="ts" setup>
	import {
		faAnglesRight,
		faArrowDownAZ,
		faBoxArchive,
		faFolder,
		faHouse,
		faXmark,
		IconDefinition,
	} from '@fortawesome/free-solid-svg-icons'
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

	const route = useRoute()

	const navList: Array<{
		title: string
		icon: IconDefinition
		target: string
	}> = [
		{
			title: 'Content Management',
			icon: faHouse,
			target: '/',
		},
		{
			title: 'Course Management',
			icon: faFolder,
			target: '/course-management',
		},
	]

	// NOTE - DashBoard handler
	const isDashBoardExpanded = ref<boolean>(false)
	const onClickScaleDashBoard = () => {
		isDashBoardExpanded.value = !isDashBoardExpanded.value
	} // onClickScaleDashBoard

	watch(
		() => route.fullPath,
		() => {
			if (isDashBoardExpanded.value) onClickScaleDashBoard()
		},
		{
			immediate: false,
		}
	)
</script>

<template>
	<section
		class="dash-board-section"
		:class="{
			'--is-expanded': isDashBoardExpanded,
		}"
	>
		<div class="dash-board-section__mask" @click="onClickScaleDashBoard" />
		<div class="dash-board-section__inner">
			<div class="dash-board-header">
				<div class="dash-board-header__head-block flex items-center">
					<div class="control">
						<button class="scale-btn" @click="onClickScaleDashBoard">
							<FontAwesomeIcon
								:icon="isDashBoardExpanded ? faXmark : faAnglesRight"
								class="scale-icon"
							/>
						</button>
					</div>
					<div class="title">School Resources</div>
				</div>

				<div class="dash-board-header__body-block">
					<div class="control">
						<button
							v-if="route.name === ROUTER_HOME_NAME"
							class="page-btn upload-btn"
						>
							<div class="icon--outer">
								<FontAwesomeIcon :icon="faBoxArchive" class="icon" />
							</div>
							<div class="title">New Upload</div>
						</button>

						<div>
							<button
								v-if="route.name === ROUTER_HOME_NAME"
								class="page-btn upload-btn"
							>
								<div class="icon--outer">
									<FontAwesomeIcon :icon="faArrowDownAZ" class="icon" />
								</div>
								<div class="title">Sort</div>
							</button>
						</div>
					</div>
				</div>
			</div>

			<div class="dash-board-body">
				<div class="dash-board-body__head-block">
					<div class="title">School Resources</div>
				</div>
				<!-- .dash-board-body__header -->

				<div class="dash-board-body__nav">
					<div class="list">
						<router-link v-for="item in navList" :to="item.target" class="item">
							<div class="icon--outer">
								<FontAwesomeIcon :icon="item.icon" class="icon" />
							</div>
							<span class="title">
								{{ item.title }}
							</span>
						</router-link>
					</div>
				</div>
				<!-- .dash-board-body__nav -->
			</div>
		</div>
	</section>
</template>

<style lang="scss">
	.dash-board-section {
		position: absolute;
		left: 0;
		top: 0;
		height: 100%;
		z-index: 10;

		@media screen and (min-width: $screen-1024) {
			position: static;
			min-height: 100vh;
			width: 256px;
			flex: 0 0 256px;
		}

		&__mask {
			position: absolute;
			display: none;
			background-color: rgba($gray-color-300, 0.5);
			left: 0;
			top: 0;
			height: 100%;
			width: 100%;
			z-index: -1;

			@media screen and (min-width: $screen-1024) {
				display: none;
			}
		}

		&__inner {
			width: 50px;
			height: 100%;
			background-color: #fff;
			overflow: hidden;
			position: fixed;
			top: 0;

			@media screen and (min-width: $screen-1024) {
				width: 256px;
				top: 8px;
				height: calc(100vh - 16px);
				border-radius: 8px;
			}
		}

		&.--is-expanded {
			@media screen and (max-width: ($screen-1024 - 1)) {
				width: 100%;

				.dash-board-section__mask {
					display: block;
				}

				.dash-board-section__inner {
					width: 240px;
				}
			}
		}
	}

	.dash-board-header {
		position: relative;
		min-height: 102px;
		padding-bottom: 20px;

		&:before {
			content: '';
			display: block;
			position: absolute;
			left: 0;
			bottom: 0;
			width: 100%;
			height: 1px;
			background: linear-gradient(
				90deg,
				rgba(224, 225, 226, 0) 0%,
				#e0e1e2 49.52%,
				rgba(224, 225, 226, 0.15625) 99.04%
			);
		}

		&__head-block {
			display: flex;

			@media screen and (min-width: $screen-1024) {
				display: none;
			}

			.control {
				min-width: 0;
				@media screen and (min-width: $screen-1024) {
					display: none;
				}
			}

			.scale-btn {
				width: 52px;
				height: 56px;
				background-color: $gray-color-200;
			}

			.scale-icon {
				font-size: $font-size-lg;
				color: $gray-color-300;
			}

			.title {
				flex: 1 1 0;
				font-size: $font-size-md;
				font-weight: 700;
				overflow: hidden;
				white-space: nowrap;
				text-overflow: ellipsis;
				margin-left: 16px;
			}
		}

		&__body-block {
			margin-top: 10px;

			.control {
				padding: 0 2px;
				margin-top: 4px;
			}

			.page-btn {
				width: 100%;
				display: flex;
				align-items: center;
				justify-content: start;
				margin-bottom: 4px;
				background-color: $gray-color-200;
				border-radius: 8px;

				@media screen and (min-width: $screen-1024) {
					display: none;
				}

				&:last-child {
					margin-bottom: 0;
				}

				&.upload-btn {
					background-color: $blue-color;
					color: #fff;
				}

				.icon--outer {
					display: inline-flex;
					height: 48px;
					width: 48px;
					flex: 0 0 48px;
					align-items: center;
					justify-content: center;
					min-width: 0;
				}
				.icon {
					font-size: $font-size-md;
				}
				.title {
					font-size: 13px;
					flex: 1 1 0;
					font-weight: 700;
					max-width: 100%;
					overflow: hidden;
					text-overflow: ellipsis;
					text-align: left;
				}
			}
		}
	}

	.dash-board-body {
		padding-top: 16px;

		&__head-block {
			.title {
				display: none;
				font-weight: 700;
				font-size: $font-size-md;
				padding: 0 24px;
				margin-bottom: 12px;

				@media screen and (min-width: $screen-1024) {
					display: block;
				}
			}
		}

		&__nav {
			.list {
				padding: 0 2px;

				@media screen and (min-width: $screen-1024) {
					padding: 0 10px;
				}
			}

			.item {
				width: 100%;
				display: flex;
				align-items: center;
				justify-content: start;
				margin-bottom: 4px;
				background-color: $gray-color-200;
				border-radius: 8px;
				color: $gray-color-300;

				&:last-child {
					margin-bottom: 0;
				}

				&.--is-active {
					background-color: $blue-color;
					color: #fff;
				}
			}

			.icon--outer {
				display: inline-flex;
				height: 48px;
				width: 48px;
				flex: 0 0 48px;
				align-items: center;
				justify-content: center;
				min-width: 0;
			}

			.icon {
				font-size: $font-size-md;
			}

			.title {
				font-size: 13px;
				font-weight: 700;
				flex: 1 1 0;
				max-width: 100%;
				display: -webkit-box;
				-webkit-box-orient: vertical;
				-webkit-line-clamp: 2;
				overflow: hidden;
				text-overflow: ellipsis;
			}
		}
	}
</style>
