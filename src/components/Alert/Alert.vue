<template>
	<transition name="slide-fade">
		<div
			v-if="(isGlobal && getAlert.showAlert) || !isGlobal"
			@click="closeAlert"
			class="alert"
			:class="[alertModifierClass, isGlobal ? 'alert--global' : '']"
		>
			<span class="alert__icon">
				<AlertIcon :type="alertType" />
			</span>
			<div class="alert__container" :class="containerModifierClass">
				<span class="alert__title">
					<template v-if="getAlert.showAlert">{{ getAlert.title || getAlert.status }}!</template>
					<slot v-else name="title">{{ alertType }}</slot>
				</span>
				<p class="alert__text">
					<slot>{{ getAlert.message }}</slot>
				</p>
			</div>
			<c-button v-if="showAction" @click.native="$emit('action')" class="ml-auto alert__cta" :buttonType="actionBtnType"
				>Resend Title</c-button
			>
		</div>
	</transition>
</template>

<script src="./Alert.js"></script>
<style lang="scss" scoped src="./Alert.scss"></style>
