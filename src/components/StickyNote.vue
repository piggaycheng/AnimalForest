<template>
	<div class="col-md-3">
		<div class="card">
			<h5 class="card-title">{{ noteData.title }}</h5>
			<div
				class="card-body"
				@mouseover.stop="hover($event, true)"
				@mouseout.stop="hover($event, false)"
				@click="clickCard"
			>{{ noteData.content }}</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "StickyNote",
	props: ["noteData"],
	data: function() {
		return {
			isHovering: false
		};
	},
	methods: {
		hover(e, isHovering) {
			if (isHovering) {
				e.target.parentElement.classList += " shadow rounded";
			} else {
				e.target.parentElement.className = "card";
			}
		},
		clickCard() {
			this.$emit("click-card", this.noteData);
		}
	}
};
</script>

<style>
.card {
	margin: 0.5rem;
	height: 15rem;
	padding-top: 1rem;

    /* card rotate animation */
	-webkit-transition: -webkit-transform 0.5s;
	transition: transform 0.5s;

    background-color: #FBF5A9 !important;
}

.card-body {
	text-align: start;
}

.card:hover {
    /* card rotate animation */
	-webkit-transform: rotate(10deg);
	transform: rotate(10deg);
}
</style>