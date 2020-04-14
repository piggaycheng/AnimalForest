<template>
    <div class="col-md-3">
        <div class="card">
            <h5 class="card-title">{{ noteData.title }}</h5>
            <div class="card-body" @mouseover.stop="hover($event, true)" @mouseout.stop="hover($event, false)" @click="clickCard">
                {{ noteData.content }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'StickyNote',
    props: ['noteData'],
    data: function () {
        return {
            isHovering: false,
        }
    },
    methods: {
        hover(e, isHovering) {
            if(isHovering) {
                e.target.parentElement.classList += ' shadow bg-white rounded';
            } else {
                e.target.parentElement.className = 'card';
            }
        }, 
        clickCard() {
            this.$emit('click-card', this.noteData);
        }
    },
}
</script>

<style>
.card {
    margin: 0.5rem;
    height: 15rem;
    padding-top: 1rem;
}

.card-body {
    text-align: start;
}
</style>