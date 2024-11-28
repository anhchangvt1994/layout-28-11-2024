<script lang="ts" setup>
	import { faAngleLeft, faAngleRight } from '@fortawesome/free-solid-svg-icons'
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
	import router from 'app/router'

	const props = defineProps<{
		total: number
	}>()

	const route = useRoute()

	const curPage = ref<number>(
		route.query && route.query.page ? Number(route.query.page) : 1
	)

	const pagesToShow = ref<Array<number | string>>([])

	const formatPagesToShow = () => {
		if (!props.total) return

		if (props.total <= 3) {
			if (!pagesToShow.value.length) {
				for (let i = 0; i < props.total; i++) {
					pagesToShow.value.push(i + 1)
				}
			}
			return
		}

		if (curPage.value === 2) pagesToShow.value = [1, 2, '...', props.total]
		else if (curPage.value === props.total - 1)
			pagesToShow.value = [1, '...', props.total - 1, props.total]
		else pagesToShow.value = [1, '...', curPage.value, '...', props.total]
	} // formatPagesToShow

	const onClickChangePage = (page: number) => {
		if (!page) return

		curPage.value = page
	} // onClickChangePage

	const onClickPrevBtn = () => {
		if (curPage.value === 1) return
		curPage.value = curPage.value - 1
		router.push(`/?page=${curPage.value}`)
	} // conClickPrevBtn

	const onClickNextBtn = () => {
		if (curPage.value === props.total) return
		curPage.value = curPage.value + 1
		router.push(`/?page=${curPage.value}`)
	} // conClickNextBtn

	formatPagesToShow()

	watch(
		() => curPage.value,
		() => {
			formatPagesToShow()
		},
		{
			immediate: false,
		}
	)
</script>

<template>
	<div class="home-page__break-page-group">
		<button
			class="home-page__break-page-btn home-page__break-page-btn--prev"
			:class="{
				'--is-disable': !props.total || curPage === 1,
			}"
			@click="onClickPrevBtn"
		>
			<FontAwesomeIcon :icon="faAngleLeft" />
		</button>

		<RouterLink
			v-for="val in pagesToShow"
			:key="val"
			class="home-page__break-page-btn home-page__break-page-btn"
			:class="{
				'--is-active': val === curPage,
			}"
			:to="`?page=${val}`"
			@click="()=>onClickChangePage(val as number)"
		>
			{{ val }}
		</RouterLink>

		<button
			class="home-page__break-page-btn home-page__break-page-btn--next"
			:class="{
				'--is-disable': !props.total || curPage === props.total,
			}"
			@click="onClickNextBtn"
		>
			<FontAwesomeIcon :icon="faAngleRight" />
		</button>
	</div>
	<!-- .home-page__break-page-group -->
</template>

<style lang="scss">
	.home-page {
		&__break-page-group {
			display: flex;
			gap: 8px;
		}

		&__break-page-btn {
			display: inline-flex;
			flex: 0 0 34px;
			width: 34px;
			height: 34px;
			justify-content: center;
			align-items: center;
			border-radius: 50%;
			border: 1px solid #8392ab;
			box-shadow: 0px 4px 6px 0px #00000014;

			&.--is-disable {
				-webkit-user-select: none; /* Safari */
				-ms-user-select: none; /* IE 10 and IE 11 */
				user-select: none; /* Standard syntax */
				opacity: 0.3;
			}

			&.--is-active {
				background-color: $blue-color;
				border-color: $blue-color;
				box-shadow: 0px 4px 6px 0px #00000014;
				color: #fff;
			}
		}
	}
</style>
