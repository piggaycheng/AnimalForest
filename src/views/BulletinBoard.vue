<template>
	<div class="bulletin-board container-fluid">
		<div class="row">
			<StickyNote v-for="(item, index) in testData" :key="index" @click-card="clickCard" :noteData="item"></StickyNote>
		</div>
		<button class="btn btn-success btn-circle m-1" data-toggle="modal" data-target="#modal" @click="clickAddBtn"><i class="fas fa-plus"></i></button>
		<Modal :title="modalTitle" :modalType="modalType" ref="modal" @click-edit="clickEditBtn">
			<form slot="modalBody" v-if="isForm">
				<label for="title">標題</label>
				<input class="form-control" id="stickyFormTitle" type="text" placeholder="Default input">
				<label for="title">內容</label>
				<textarea class="form-control" id="stickyFormContent" rows="5"></textarea>
			</form>
			<div slot="modalBody" v-else>
				{{ modalContent }}
			</div>
		</Modal>
	</div>
</template>

<script>
// @ is an alias to /src
import StickyNote from '@/components/StickyNote.vue'
import Modal from '@/components/Modal.vue'
import $ from 'jquery';

export default {
	name: 'BulletinBoard',
	components: {
		StickyNote,
		Modal
	},
	data: function () {
        return {
			modalTitle: "",
			isForm: false,
			modalType: "",
			modalContent: "",
			testData: [
				{id: 1, title: 'testTitle1', content: 'testContent bra bra bra', deadTime: ''},
				{id: 2, title: 'testTitle2', content: 'testContent bra bra bra', deadTime: ''},
				{id: 3, title: 'testTitle3', content: 'testContent bra bra bra', deadTime: ''},
				{id: 4, title: 'testTitle4', content: 'testContent bra bra bra', deadTime: ''}
			]
        }
    },
	methods: {
		clickCard(noteData) {
			this.isForm = false;
			this.modalTitle = noteData.title;
			this.modalType = "preview";
			this.modalContent = noteData.content;
			$(this.$refs.modal.$el).modal('show');
		},
		clickAddBtn() {
			this.isForm=true;
			this.modalType = 'form';
			this.modalTitle = '新增';
		},
		clickEditBtn() {
			this.isForm=true;
			this.modalType = 'form';
			console.log('edit');
		}
	}
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
	border-radius: 50% !important;
	position: fixed;
	bottom: 5rem;
	right: 5rem;
}

input {
	margin-bottom: 1rem;
}
</style>