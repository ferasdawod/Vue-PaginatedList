<template>
	<div class="item-container">
		<div class="avatar">
			<img :src="item.avatarUrl" :alt="`${item.name} profile image`" />
		</div>

		<div class="item-content">
			<h4 v-text="item.name"></h4>
			<div class="item-company">
				<span v-text="item.company"></span>
			</div>
			<div class="item-date">
				<span v-text="item.date"></span>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "HeadhunterItem",

	props: {
		item: {
			type: Object,
			required: true
		}
	}
};
</script>

<style scoped>
.item-container {
	display: block;
	overflow: auto;

	margin: 1em 0;
}

.avatar {
	float: left;
}

.avatar img {
	height: 100px;
	width: 100px;

	object-fit: cover;
}

.item-content {
	display: inline-block;
	margin-left: 1em;
	margin-top: 1em;
}

.item-content h4 {
	margin: 0 0 0.25em 0;
	color: #444;
}

.item-company {
	margin-bottom: 1em;
	color: gray;
}

.item-date {
	color: gray;
}
</style>
