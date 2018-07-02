<template>
	<div>
		<h2>Bookmark title</h2>
		<input type="text" v-model="title">
		<h2>Bookmark URL</h2>
		<input type="text" v-model="bookmarkUrl">
		<div class="button_wrap">
			<button class="cancel" @click="cancelTitle()">Cancel</button>
			<button class="save" @click="saveTitle()">Save</button>
		</div>
	</div>
</template>

<script>
	import {eventEmitter} from '../main'
	export default {
		data() {
			return {
				title: '',
				bookmarkUrl: '',
				id: '-1'
			}
		},
		methods: {
			saveTitle: function() {
				eventEmitter.$emit('saveTitle', [this.title, this.id, this.bookmarkUrl])
				this.cancelTitle()
			},
			cancelTitle() {
				this.title = '',
				this.bookmarkUrl = ''
			}
		},
		created() {
			eventEmitter.$on('bookmarkChanged', (nameObj) => {
				this.title = nameObj[0]
				this.id = nameObj[1]
				this.bookmarkUrl = nameObj[2]
				console.log(nameObj[1])
			})
		}
	}
</script>

<style scoped>
	.button_wrap {
		margin-top: 20px;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	button {
		border: 1px solid rgba(0, 0, 0, .2);
		background-color: transparent;
		padding: 10px 20px;
		border-radius: 5px;
		text-transform: lowercase;
		transition: all 0.4s ease;
	}
	button:hover {
		background-color: #5eb957;
		color: #fff;
	}
	h2 {
		font-size: 16px;
		font-weight: 400;
		padding: 0;
	}
	input {
		margin-bottom: 20px;
	}
</style>