<script lang="ts" setup>
	import { faTags, faXmarkCircle } from '@fortawesome/free-solid-svg-icons'
	import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

	const tagList = ref<Array<string>>([])
	const searchTagInputVal = ref<string>()
	const isSearchTagBarActive = ref<boolean>(false)
	const elSearchTagInput = useTemplateRef<HTMLInputElement, string>(
		'search-tag-input'
	)

	const onFocus = (() => {
		let timeout
		return (type: 'out' | 'in') => {
			if (!type) return

			if (type === 'in') {
				if (timeout) clearTimeout(timeout)
				isSearchTagBarActive.value = true
				if (elSearchTagInput.value) {
					elSearchTagInput.value.focus()
				}
			} else if (type === 'out') {
				if (timeout) clearTimeout(timeout)
				timeout = setTimeout(() => {
					isSearchTagBarActive.value = false
				}, 10)
			}
		}
	})() // onFocus

	const onKeypressSearchTagInput = (e) => {
		if (e.key === 'Enter') {
			if (!searchTagInputVal.value) return

			tagList.value.push(searchTagInputVal.value)
			searchTagInputVal.value = ''
		} else if (e.key === 'Backspace') {
			if (searchTagInputVal.value || !tagList.value.length) return

			tagList.value.pop()
		}
	} // onKeypressSearchTagInput

	const onRemoveSearchTag = (index: number) => {
		if (typeof index !== 'number' || !tagList.value.length) return

		if (elSearchTagInput.value) {
			elSearchTagInput.value.focus()
		}

		tagList.value = tagList.value.filter((val, idx) => idx !== index)
	} // onRemoveSearchTag
</script>

<template>
	<div class="search-tag-bar">
		<div
			class="search-tag-bar--inner"
			:class="{
				'--is-active': isSearchTagBarActive,
			}"
			@click="() => onFocus('in')"
			@focusout="() => onFocus('out')"
		>
			<input
				class="search-tag-bar__input"
				type="text"
				placeholder="Search by Tags..."
				v-model="searchTagInputVal"
				@keyup="onKeypressSearchTagInput"
				ref="search-tag-input"
			/>
			<div class="search-tag-bar__tag-list">
				<template v-for="(tagMessage, id) in tagList">
					<span v-if="tagMessage" class="search-tag-bar__tag-item">
						<span class="search-tag-bar__tag-message-label">{{
							tagMessage
						}}</span>
						<button class="search-tag-bar__remove-tag-btn">
							<FontAwesomeIcon
								:icon="faXmarkCircle"
								class="ml-4"
								@click="() => onRemoveSearchTag(id)"
							/></button
					></span>
				</template>
			</div>
			<div class="search-tag-bar__box" />
			<div class="search-tag-bar__icon--outer">
				<FontAwesomeIcon :icon="faTags" class="search-tag-bar__icon" />
			</div>
		</div>
	</div>
	<!-- .search-tag-bar -->
</template>

<style lang="scss">
	.search-tag-bar {
		display: flex;
		position: relative;
		height: 32px;
		z-index: 1;

		@media screen and (min-width: $screen-1024) {
			height: 40px;
		}

		&--inner {
			position: absolute;
			display: flex;
			flex-wrap: wrap;
			left: 0;
			top: 0;
			height: 32px;
			width: 100%;
			padding-left: 8px;
			padding-right: 26px;
			overflow: hidden;

			@media screen and (min-width: $screen-1024) {
				height: 40px;
			}

			&.--is-active {
				height: auto;
				min-height: 100%;

				.search-tag-bar__box {
					border-radius: 8px;
					border-color: #2563eb;
					height: auto;
					min-height: 100%;
				}

				.search-tag-bar__icon--outer {
					border-top-left-radius: 8px;
					border-bottom-left-radius: 8px;

					.search-tag-bar__icon {
						color: $blue-color;
					}
				}

				.search-tag-bar__icon--inner {
					height: auto;
					min-height: 100%;
				}

				.search-tag-bar__tag-list {
					display: inline-flex;
					flex-wrap: wrap;

					.search-tag-bar__tag-item {
						margin-right: 0;
					}
				}
			}
		}

		&__tag-list {
			display: inline-block;
			gap: 4px;
			align-items: center;
			order: 0;
			padding: 6px 8px 6px 0;
			min-height: 100%;
			max-width: 100%;
			overflow: hidden;
			white-space: nowrap;
			text-overflow: ellipsis;

			&:has(.search-tag-bar__tag-item) {
				display: block;
			}
		}

		&__tag-item {
			display: inline-flex;
			align-items: center;
			height: 20px;
			font-size: 13px;
			padding: 0 4px 0 8px;
			background-color: #828282;
			color: #fff;
			border-radius: 12px;
			margin-right: 4px;

			&:last-child {
				margin-right: 0;
			}
		}

		&__tag-message-label {
			display: inline-block;
			max-width: 50px;
			overflow: hidden;
			text-overflow: ellipsis;
		}

		&__remove-tag-btn {
			display: inline-flex;
			align-items: center;
			color: #fff;
			margin-left: 4px;
		}

		&__icon--outer {
			position: absolute;
			right: 0;
			top: 0;
			display: inline-flex;
			align-items: center;
			height: 100%;
			min-width: 0;
			padding-right: 16px;
			padding-right: 12px;
			border-top-left-radius: 4px;
			border-bottom-left-radius: 4px;
		}

		&__icon {
			font-size: $font-size-md;
			color: $gray-color-400;
		}

		&__input {
			order: 1;
			font-size: 13px;
			height: 32px;
			padding: 6px 0;

			@media screen and (min-width: $screen-1024) {
				height: 40px;
			}

			&::placeholder {
				color: #828282;
			}

			&:focus {
				font-family: 'Poppins', 'sans-serif';

				&::placeholder {
					color: $blue-color;
					font-weight: 700;
				}
			}
		}

		&__box {
			position: absolute;
			top: 0;
			left: 0;
			width: 100%;
			height: 32px;
			z-index: -2;
			background-color: #fff;
			border: 1px solid #d6d6d6;
			border-radius: 4px;

			@media screen and (min-width: $screen-1024) {
				height: 40px;
			}
		}
	}
</style>
