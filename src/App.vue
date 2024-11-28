<script setup lang="ts">
	import DashBoard from 'components/DashBoard.vue'
	import Header from 'components/Header.vue'
</script>

<template>
	<div class="layout">
		<div class="main-container">
			<DashBoard />
			<div class="main-content">
				<Header />
				<div class="main-body">
					<RouterView v-slot="{ Component }">
						<template v-if="Component">
							<Suspense>
								<component :is="Component"></component>
							</Suspense>
						</template>
					</RouterView>
				</div>
			</div>
		</div>
		<!-- .main-container -->
	</div>
	<!-- .layout -->
</template>

<style lang="scss">
	.main-container {
		position: relative;
		max-width: 100%;
		min-width: 0;
		min-height: 100vh;
		/* overflow: hidden; */
		padding: 8px;
		margin: 0 auto;
		background-color: $gray-color-100;
		padding-left: 58px;

		@media screen and (min-width: $screen-1024) {
			display: flex;
			max-width: 1440px;
			padding: 0;
			gap: 8px;
			padding: 8px;
		}
	}

	.main-content {
		flex: 1 1 auto;
	}

	.main-body {
		min-height: calc(100vh - 58px);
		background-color: #fff;
		border-top-left-radius: 8px;
		padding: 8px 16px;
		margin-right: -8px;

		@media screen and (min-width: $screen-1024) {
			margin-right: 0;
			border-radius: 8px;
		}
	}
</style>
