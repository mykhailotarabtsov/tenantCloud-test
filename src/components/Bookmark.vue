<template>
	<div>
		<!-- <div class="bookmarks">
			<h2>{{ h2 }}</h2>
			<div class="bookmarks__bookmark">
				<h3 class="bookmarks__bookmark-title">{{ bookmarkTitle }}</h3>
				<button class="bookmarks__bookmark-edit-btn">Edit</button>
			</div>
		</div> -->
		<div class="bookmarks">
			<h2>{{ h2 }}</h2>
			<!-- <app-bookmarks-list
				v-for="item in bookmarksArray"
				:key="item.id"
				:bookmarkTitle="item.title"
				:bookmarkId="item.id"
				v-on:bookmarkChanged="item.title = $event"
			></app-bookmarks-list> -->
			<ul>
				<li 
					v-for="item in filteredbookmarksArray"
					:key="item.id"
					:bookmarkTitle="item.title"
					:bookmarkId="item.id"
					v-on:bookmarkChanged="item.title = $event"
				><a :href="item.link">{{ item.title }}</a> <button @click="changeBookmark(item.id, item.title, item.link)"  class="bookmarks__bookmark-edit-btn">Edit</button></li>
			</ul>
		</div>
		<button class="bookmarks__bookmark-edit-btn" @click="addBookmark()">Create bookmark</button>
		<input v-bind:class="{'input__change-bookmark': true, 'display__none': display__active}" type="text" @keyup.enter="addBookmarkInput()" v-model="valueInput">
	</div>
</template>

<script>
	import MyBookmarksList from './BookmarksList.vue'
	import {eventEmitter} from '../main'
	export default {
		name: 'MyBookmark',
		props: ['searchValueFrom'],
		data () {
			return {
				h2: 'Bookmark list',
			  bookmarksArray: [
					{
						id: 0,
						title: "Bookmark title",
						link: "http://google.com"
					},
					{
						id: 1,
						title: "Bookmark title",
						link: "http://youtube.com"
					},
					{
						id: 2,
						title: "Bookmark title one",
						link: "http://facebook.com"
					},
					{
						id: 3,
						title: "Bookmark title two",
						link: "http://twitter.com"
					},
					{
						id: 4,
						title: "Bookmark title three",
						link: "http://instagram.com"
					},
					{
						id: 5,
						title: "Bookmark title four",
						link: "http://ru.vuejs.org.com"
					},
					{
						id: 6,
						title: "Bookmark title five",
						link: "http://google.com.ua"
					},
					{
						id: 7,
						title: "Bookmark title six",
						link: "http://google.com"
					}
				],
				display__active: true,
				valueInput: '',
				idCount: 8
			}
		},
		components: {
			appBookmarksList: MyBookmarksList
		},
		methods: {
			addBookmark: function() {
				this.display__active = !this.display__active;
				// this.valueInput = '';
			},
			addBookmarkInput: function() {
				console.log(this.valueInput);
				this.bookmarksArray.push({
					id: this.idCount++,
					title: this.valueInput
				});
				this.valueInput = '';
			},
			changeBookmark: function(id, title, url) {
				console.log(id + ' ' + title);
				eventEmitter.$emit('bookmarkChanged', [title, id, url]);
			}
		},
		computed: {
			filteredbookmarksArray: function() {
				var rgxp = new RegExp(this.searchValueFrom, "gi");
				return this.bookmarksArray.filter((bookmark) => {
					return bookmark.title.match(rgxp);
				});
			}
		},
		beforeCreate() {
			eventEmitter.$on('saveTitle', (saveObj) => {
				for(var i = 0; i < this.bookmarksArray.length; i++) {
					if ( this.bookmarksArray[i].id == saveObj[1] ) {
						// this.bookmarksArray[i].title = saveObj[0]
						var newObj = {id: saveObj[1], title: saveObj[0], link: saveObj[2]}
						console.log(newObj)
						this.bookmarksArray.splice(i, 1, newObj)
						console.log(this.bookmarksArray[i])
						console.log(i)
						// console.log(saveObj[0])
						// console.log(this.bookmarksArray[i].title)
					} 
				}
			})
		}
	}
</script>
<style>
	.bookmarks {
		border: 1px solid #000;
		padding: 5px;
		margin-bottom: 20px;
	}
	h2 {
		padding-left: 20px;
		margin: 0;
		margin-bottom: 10px;
	}
	.bookmarks__bookmark-edit-btn {
		border: none;
		outline: none;
		background: none;
		color: #6fd02a;
		font-size: 1.1em;
		cursor: pointer;
	}
	ul {
		list-style-type: none;
		padding: 0;
		margin: 0;
	}
	ul li {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	ul li a {
		text-decoration: none;
		color: #000;
		cursor: pointer;
	}
	.display__none, .h3_display_none {
		display: none;
	}
</style>