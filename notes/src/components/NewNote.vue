<template>
	<div class="new-note">
		<label>Title</label>
		<input v-model="note.title" type="text" />
		<div class="note-priority">
			<div class="note-priority-item">
				<input type="radio" id="priority-normal" v-model="note.priority" value="normal">
				<label for="priority-normal">
					Normal
				</label>
			</div>
			<div class="note-priority-item">
				<input type="radio" id="priority-important" v-model="note.priority" value="important">
				<label for="priority-important">
					Important
				</label>
			</div>
			<div class="note-priority-item">
				<input type="radio" id="priority-super-important" v-model="note.priority" value="super-important">
				<label for="priority-super-important">
					Super Important
				</label>
			</div>

		</div>
		<label>Description</label>
		<textarea v-model="note.descr"></textarea>
		<button class="btn btnPrimary" @click="addNote">New note</button>
	</div>
</template>

<script>
export default {
	props: {
		note: {
			type: Object,
			required: true,
		},
	},
	methods: {
		addNote() {
			this.$emit("addNote", this.note);
		},
	},
};
</script>

<style lang="scss">
.new-note {
	text-align: center;

}
.note-priority {
	display: flex;
	justify-content: space-around;
	&-item {
		display: flex;
		align-items: baseline;
		& input {
			width: auto;
			margin-right: 20px;
		}
	}
}

</style>
