<template>
	<div class="container">
		<div>
			<headhunters :items="headhunters" />
		</div>
	</div>
</template>

<script>
import Headhunters from "./components/headhunter/Headhunters";

export default {
	name: "Index",

	components: {
		Headhunters
	},

	computed: {
		headhunters() {
			const items = [];

			for (let index = 0; index < 11; index++) {
				items.push({
					id: index,
					...this.generateHeadhunter(index + 1)
				});
			}

			return items;
		}
	},

	methods: {
		generateHeadhunter(index) {
			return {
				name: `Headhunter ${index} Name`,
				company: `Example company ${index} name`,
				avatarUrl: "https://i.pravatar.cc/500",
				date: "15, April 2019"
			};
		}
	}
};
</script>

<style scoped>
.container {
	margin: 16px;

	font-family: sans-serif;
}
</style>
