<template>
	<div>
		<h2>{{ h2 }}</h2>
		<div class="users">
			<div class="users__user">
				<div class="users__user-flex-wrap">
					<div class="users__user-avatar"></div>
					<div class="users__user-inform">
						<h3>{{ firstName }}</h3>
						<p>Email</p>
					</div>
				</div>
				<button class="users__user-edit-btn">Edit</button>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'MyPeople',
		data () {
			return {
				h2: 'People',
				firstName: 'Mykhailo'
			}
		}
	}
</script>
<style>
	.users {
		border: 1px solid #000;
		padding: 10px;
	}
	.users__user {
		display: flex;
		justify-content: space-between;
		align-items: center;
		background-color: #ecedf1;
		padding: 10px;
		padding-right: 30px;
	}
	.users__user-flex-wrap {
		display: flex;
		align-items: center;
	}
	.users__user-avatar {
		display: block;
		width: 50px;
		height: 50px;
		border-radius: 50%;
		border: 1px solid #000;
		background: url('../assets/logo.png') no-repeat 50% 50%;
		background-size: cover;
		margin-right: 20px;
	}
	.users__user-inform h3 {
		margin-bottom: 5px;
	}
	.users__user-inform p {
		margin-top: 0;
		color: #696969;
	}
	.users__user-edit-btn {
		border: none;
		outline: none;
		background: none;
		color: #6fd02a;
		font-size: 1.1em;
	}
</style>