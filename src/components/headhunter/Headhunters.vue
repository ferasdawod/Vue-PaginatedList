<template>
	<section
		class="container"
		@mouseenter="onMouseEnter"
		@mouseleave="onMouseLeave"
	>
		<!-- Title -->
		<div class="title">
			<h3>Headhunter auf Ihrem Profil</h3>
			<span>Diese Headhunter haben Interesse</span>
		</div>

		<!-- Items -->
		<div class="items">
			<template v-for="item in displayedItems">
				<keep-alive>
					<headhunters-item :item="item" :key="item.id" />
				</keep-alive>
			</template>
		</div>

		<!-- Footer -->
		<div class="footer">
			<span>10 Headhunter-Besuche insgesamt</span>
		</div>

		<!-- Controls -->
		<transition name="fade">
			<div v-if="ui.isMouseOver" class="controls">
				<button :disabled="!hasPreviousPage" @click="onPrevPageClick">▲</button>
				<button :disabled="!hasNextPage" @click="onNextPageClick">▼</button>
			</div>
		</transition>
	</section>
</template>

<script>
import HeadhuntersItem from "./HeadhuntersItem";

export default {
	name: "HeadHunter",

	perPageItems: 3,

	components: {
		HeadhuntersItem
	},

	props: {
		items: {
			type: Array,
			required: true
		}
	},

	data: () => ({
		ui: {
			isMouseOver: false,
			page: 0
		}
	}),

	computed: {
		displayedItems() {
			const startIndex = this.ui.page * this.$options.perPageItems;
			const endIndex = startIndex + this.$options.perPageItems;

			return this.items.slice(startIndex, endIndex);
		},

		hasPreviousPage() {
			return this.ui.page > 0;
		},

		hasNextPage() {
			return (
				this.ui.page * this.$options.perPageItems + this.$options.perPageItems <
				this.items.length
			);
		}
	},

	methods: {
		onMouseEnter() {
			this.ui.isMouseOver = true;
		},

		onMouseLeave() {
			this.ui.isMouseOver = false;
		},

		onPrevPageClick() {
			this.ui.page--;
		},

		onNextPageClick() {
			this.ui.page++;
		}
	}
};
</script>

<style scoped>
.container {
	position: relative;
	display: inline-block;
	border: 1px solid lightgray;
	padding: 1em 4em 1em 1em;
}

.title h3 {
	margin: 0 0 0.5em 0;
	color: #444;
}

.title span {
	color: gray;
}

.items {
	margin: 1em 0;
}

.footer span {
	color: gray;
}

.controls {
	position: absolute;
	right: 0.5em;

	top: 0;
	bottom: 0;
	margin: auto;

	height: 132px;
}

.controls button {
	display: block;
	border: none;

	height: 60px;
	width: 40px;

	margin: 4px;

	border-radius: 4px;
	background: #888;
	color: white;
}

.controls button:disabled {
	opacity: 0.5;
}

.fade-enter-active,
.fade-leave-active {
	transition: opacity 0.2s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
	opacity: 0;
}
</style>
