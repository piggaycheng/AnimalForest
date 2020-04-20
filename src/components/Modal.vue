<template>
    <!-- Modal -->
    <div class="modal fade" id="modal" tabindex="-1" role="dialog">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">{{ title }}</h5>
                    <button type="button" class="close" data-dismiss="modal">
                        <span>&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <slot name="modalBody"></slot>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary" v-if="modalType == 'form'" @click="clickSave">Save changes</button>
                    <button type="button" class="btn btn-primary" v-if="modalType == 'preview'" @click="clickEdit">Edit</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Modal',
    data: function () {
        return {
            
        }
    },
    props: ['title', 'modalType'],
    methods: {
        clickEdit() {
            this.$emit('click-edit');
        },
        clickSave() {
            this.$emit('click-save');
        },
    },
}
</script>

<style>
.modal {
    text-align: left;
}
</style>