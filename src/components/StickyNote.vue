<template>
    <div class="col-md-3">
        <div class="card">
            <div class="card-body" @mouseover.stop="hover($event, true)" @mouseout.stop="hover($event, false)">
                This is some text within a card body.
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'StickyNote',
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
        }
    },
}
</script>

<style>
.card {
    margin: 0.5rem;
    height: 15rem;
}
</style>