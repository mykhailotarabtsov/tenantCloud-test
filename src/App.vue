<template>
	<div>
		<div class="header">
			<h1>{{ msg }}</h1>
			<div class="header__logo"></div>
			<input v-model="searchValue" type="text" placeholder="Search" class="header__searchInput">
		</div>
	
		<div class="content">
			<div class="wrap__right-components">
				<app-bookmark
					:searchValueFrom="this.searchValue"
				></app-bookmark>
			</div>
		</div>

		<div>
			<div class="wrap__right-components">
				<h1>Edit</h1>
				<div class="edit_wrap">
					<app-edit></app-edit>
				</div>
			</div>
		</div>
	</div>
  
</template>

<script>
import MyPeople from './components/People.vue'
import MyBookmark from './components/Bookmark.vue'
import EditBookmark from './components/EditBookmark.vue'

export default {
  name: 'app',
  data () {
    return {
			msg: 'Website page part',
			searchValue: ''
    }
	},
	components: {
		appPeople: MyPeople,
		appBookmark: MyBookmark,
		appEdit: EditBookmark
	}
}
</script>

<style>
	body {
		font-size: 16px;
		font-family: sans-serif;
	}
	h1 {
		display: inline-block;
	}
	.wrap__right-components {
		width: 70%;
		float: right;
	}
	.header {
		border: 1px solid #000;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 0 30px;
	}
	.header__logo {
		width: 45px;
		height: 45px;
		border-radius: 50%;
		border: 1px solid #000;
		background: url('./assets/logo.png') no-repeat 50% 50%;
		background-size: cover;
	}
	.header__searchInput {
		width: 60%;
	}
	.content {
		border: 1px solid #000;
		padding: 20px 30px;
	}
	.content:after {
		content: '';
		display: table;
		clear: both;
	}
	.edit_wrap {
		border: 1px solid #000;
		padding: 20px 30px;
	}
	input {
		padding: 5px 10px;
	}
</style>
