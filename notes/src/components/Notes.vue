<template>
	<div class="notes">
		<div
			class="note"
			:class="[`priority-${note.priority}`, { full: !grid }]"
			v-for="(note, index) in notes"
			:key="index"
		>
			<div class="note-header" :class="{ full: !grid }">
				<div class="note-header__title">
					<input
						v-if="note.edit"
						type="text"
						:value="note.title"
						@input="inputTitle($event)"
						@keyup.enter="updateTitle(editedNote.title, index)"
						@keyup.esc="isEdit('', index)"
						v-focus
					/>
					<div v-else>
						<p @click="isEdit(note.title, index)">
							{{ note.title }}
						</p>
					</div>
				</div>
				<p style="cursor: pointer" @click="removeNote(index)">x</p>
			</div>
			<div class="note-body">
				<p>{{ note.descr }}</p>
				<span>{{ note.date }}</span>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		notes: {
			type: Array,
			required: true,
		},
		grid: {
			type: Boolean,
			required: true,
		},
	},
	data() {
		return {
			editedNote: {
				title: "",
			},
		};
	},
	methods: {
		removeNote(index) {
			this.$emit("remove", index);
		},
		updateTitle(value, index) {
			this.$emit("updateTitle", value, index);
		},
		isEdit(value, index) {
			this.editedNote.title = value;
			this.$emit("isEdit", index);
		},
		inputTitle(e) {
			this.editedNote.title = e.target.value;
		},
	},
	directives: {
		focus: {
			inserted(el) {
				el.focus();
			},
		},
	},
};
</script>

<style lang="scss">
.notes {
	display: flex;
	align-items: center;
	justify-content: space-between;
	flex-wrap: wrap;
	padding: 40px 0;
}

.note {
	width: 48%;
	padding: 18px 20px;
	margin-bottom: 20px;
	background-color: #ffffff;
	transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
	box-shadow: 0 30px 30px rgba(0, 0, 0, 0.02);
	&:hover {
		box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
		transform: translate(0, -6px);
		transition-delay: 0s !important;
	}
	&.full {
		width: 100%;
	}
	&.priority-important {
		background-color: #e2e794;
	}
	&.priority-super-important {
		background-color: #a0d69e;
	}
}
.note-header {
	display: flex;
	align-items: baseline;
	justify-content: space-between;
	h1 {
		font-size: 32px;
	}
	p {
		font-size: 22px;
		color: #402caf;
	}
	svg {
		margin-right: 12px;
		color: #999999;
		&.active {
			color: #402caf;
		}
		&:last-child {
			margin-right: 0;
		}
	}
}

.note-body {
	p {
		margin: 20px 0;
	}
	span {
		font-size: 14px;
		color: #999999;
	}
}
</style>
