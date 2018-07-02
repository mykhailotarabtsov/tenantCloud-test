<template>
	<div>
		<div class="bookmarks__bookmark">
			<!-- <h3 v-bind:class="{'bookmarks__bookmark-title': true, 'h3_display_none': h3Active}">{{ bookmarkFromParent }}</h3> -->
			<h3 class="bookmarks__bookmark-title">{{ bookmarkFromParent }}</h3>
			<!-- <input v-bind:class="{'input__change-bookmark': true, 'display__none': display__active}" type="text" v-model="bookmarkFromParent" @keyup.enter="changeBookmark()"> -->
			<button @click="changeBookmark()"  class="bookmarks__bookmark-edit-btn">Edit</button>
		</div>
	</div>
</template>

<script>
	import {eventEmitter} from '../main'

	export default {
		name: 'MyBookmarksList',
		props: {
			bookmarkTitle: {
				type: String,
				default: 'Bookmark title default'
			},
			bookmarkId: Number
		},
		data () {
			return {
				display__active: true,
				h3Active: false,
				bookmarkFromParent: this.bookmarkTitle
			}
		},
		methods: {
			changeBookmark: function() {
				console.log(this.bookmarkFromParent);
				this.display__active = !this.display__active;
				this.h3Active = !this.h3Active;
				// this.$emit('bookmarkChanged', this.bookmarkFromParent);
				eventEmitter.$emit('bookmarkChanged', [this.bookmarkFromParent, this.bookmarkId]);
			}
		}
	}
</script>
<style>
	
	.bookmarks__bookmark {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding-right: 30px;
	}
	.bookmarks__bookmark-title {
		font-style: italic;
		margin: 0;
		font-weight: normal;
	}
	.bookmarks__bookmark-edit-btn {
		border: none;
		outline: none;
		background: none;
		color: #6fd02a;
		font-size: 1.1em;
	}
	button {
		cursor: pointer;
	}
	.display__none, .h3_display_none {
		display: none;
	}

</style>