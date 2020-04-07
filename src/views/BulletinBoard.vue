<template>
	<div class="bulletin-board container-fluid">
		<div class="row">
			<StickyNote></StickyNote>
			<StickyNote></StickyNote>
			<StickyNote></StickyNote>
			<StickyNote></StickyNote>
		</div>
	</div>
</template>

<script>
// @ is an alias to /src
import StickyNote from '@/components/StickyNote.vue'

export default {
	name: 'BulletinBoard',
	components: {
		StickyNote
	}
}
</script>

<style>
.row {
    min-height: 12rem;
}
</style>