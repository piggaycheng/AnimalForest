<template>
	<div class="bulletin-board container-fluid">
		<div class="row">
			<StickyNote></StickyNote>
			<StickyNote></StickyNote>
			<StickyNote></StickyNote>
			<StickyNote></StickyNote>
		</div>
		<button class="btn btn-success btn-circle m-1" data-toggle="modal" data-target="#exampleModal" @click="isForm = true"><i class="fas fa-plus"></i></button>
		<Modal title='test'>
			<form slot="formBody" v-if="isForm">
				<label for="title">標題</label>
				<input class="form-control" id="stickyFormTitle" type="text" placeholder="Default input">
				<label for="title">內容</label>
				<textarea class="form-control" id="stickyFormContent" rows="5"></textarea>
			</form>
		</Modal>
	</div>
</template>

<script>
// @ is an alias to /src
import StickyNote from '@/components/StickyNote.vue'
import Modal from '@/components/Modal.vue'

export default {
	name: 'BulletinBoard',
	components: {
		StickyNote,
		Modal
	},
	data: function () {
        return {
            isForm: false,
        }
    },
}
</script>

<style>
.row {
    min-height: 12rem;
}

.btn-circle {
	width: 45px;
	height: 45px;
	line-height: 45px;
	text-align: center;
	padding: 0;
	border-radius: 50%;
	position: fixed;
	bottom: 5rem;
	right: 5rem;
}

input {
	margin-bottom: 1rem;
}
</style>