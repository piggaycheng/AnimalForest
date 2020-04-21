<template>
	<div class="bulletin-board container-fluid">
		<div class="row">
			<StickyNote
				v-for="(item) in dataList"
				:key="item.id"
				@click-card="clickCard(item.id, ...arguments)"
				:noteData="item"
			></StickyNote>
		</div>
		<button
			class="btn btn-success btn-circle m-1"
			data-toggle="modal"
			data-target="#modal"
			@click="clickAddBtn"
		>
			<i class="fas fa-plus"></i>
		</button>
		<Modal
			:title="modalTitle"
			:modalType="modalType"
			ref="modal"
			@click-edit="clickEditBtn"
			@click-save="clickSaveBtn"
		>
			<form slot="modalBody" v-if="isForm">
				<label for="title">標題</label>
				<input
					class="form-control"
					id="stickyFormTitle"
					type="text"
					placeholder="Default input"
					v-model="stickyFormTitle"
				/>
				<label for="title">內容</label>
				<textarea class="form-control" id="stickyFormContent" rows="5" v-model="stickyFormContent"></textarea>
			</form>
			<div slot="modalBody" v-else>{{ modalContent }}</div>
		</Modal>
	</div>
</template>

<script>
// @ is an alias to /src
import StickyNote from "@/components/StickyNote.vue";
import Modal from "@/components/Modal.vue";
import $ from "jquery";
import { db, dbTimeStamp} from "@/js/db.js";

export default {
	name: "BulletinBoard",
	components: {
		StickyNote,
		Modal
	},
	data: function() {
		return {
			isForm: false,
			modalType: "",
			modalTitle: "",
			modalContent: "",

			// form data
			stickyFormTitle: "",
			stickyFormContent: "",

			// data
			dataList: [],

			// edit data id
			editDataId: ""
		};
	},
	created() {
		let ref = db.collection("stickyNote");
		ref.onSnapshot(querySnapshot => {
			this.dataList = [];
			querySnapshot.forEach(doc => {
				let data = {
					id: doc.id,
					title: doc.data().title,
					content: doc.data().content
				};
				this.dataList.push(data);
			});
		});
	},
	methods: {
		clickCard(docId, noteData) {
			this.isForm = false;
			this.modalTitle = noteData.title;
			this.modalType = "preview";
			this.modalContent = noteData.content;
			$(this.$refs.modal.$el).modal("show");

			this.editDataId = docId;
		},
		clickAddBtn() {
			this.isForm = true;
			this.modalType = "form";
			this.modalTitle = "新增";

			this.editDataId = "";
		},
		clickEditBtn() {
			this.isForm = true;
			this.modalType = "form";
			this.stickyFormTitle = this.modalTitle;
			this.stickyFormContent = this.modalContent;
			this.modalTitle = "編輯";
		},
		clickSaveBtn() {
			let post = {
				title: this.stickyFormTitle,
				content: this.stickyFormContent,
			};

			// add
			if (this.editDataId === "") {
				let ref = db.collection("stickyNote");
				post.created = dbTimeStamp.now();
				post.updated = dbTimeStamp.now();
				
				ref.add(post).then(() => {
					console.log("add success");
					$(this.$refs.modal.$el).modal("hide");
				});
			} else {		// update
				let ref = db.collection("stickyNote").doc(this.editDataId);
				post.updated = dbTimeStamp.now();

				ref.update(post).then(() => {
					console.log("update success");
					$(this.$refs.modal.$el).modal("hide");
				});
			}
		}
	}
};
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