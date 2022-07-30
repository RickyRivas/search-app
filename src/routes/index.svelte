<script>
	// import { onMount } from 'svelte';
	import { data } from '../stores';
	let users = [];
	// get data
	data.forEach((data) => {
		users = data;
	});

	// Fetch Users
	// const fetchUsersData = async () => {
	// 	fetch('https://jsonplaceholder.typicode.com/users')
	// 		.then((res) => res.json())
	// 		.then((data) => {
	// 			users = data;
	// 		});
	// 	console.log('Fetched all users.');
	// };

	let searchTerm = '';
	let filteredSearch = [];

	const searchUsers = async () => {
		filteredSearch = users.filter((user) => {
			let name = user.name.toLowerCase();
			return name.includes(searchTerm.toLowerCase());
		});
	};
	// onMount(() => fetchUsersData());
</script>

<form action="" on:submit|preventDefault={() => {}}>
	<div class="location">
		<img src="/search.svg" alt="" width="25" height="25" />
	</div>
	<input placeholder="Search..." bind:value={searchTerm} type="search" on:input={searchUsers} />
	<!-- <button>Submit</button> -->
</form>

<sections class="users">
	{#if searchTerm && filteredSearch.length === 0}
		<h1>No users found.</h1>
	{:else if filteredSearch.length > 0}
		{#each filteredSearch as user}
			<div class="user">
				<h1>{user.name}</h1>
				<p>{user.age}</p>
				<a href={'/users/user::' + user.id}>View {user.name}'s Profile</a>
			</div>
		{/each}
	{:else}
		{#each users as user}
			<div class="user">
				<h1>{user.name}</h1>
				<p>{user.age}</p>
				<a href={'/users/user::' + user.id}>View {user.name}'s Profile</a>
			</div>
		{/each}
	{/if}
</sections>

<style lang="scss">
	.users {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		width: 100%;
		grid-gap: 0.5em;
		max-width: 1200px;
		margin: auto;
	}
	.user {
		display: flex;
		flex-direction: column;
		padding: 1em;
		border-radius: 0.5em;
		box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
	}
	/* search bar */
	form {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 2em;
		border-radius: 1em;
		position: relative;
		z-index: 2;
		width: 100%;
		max-width: 300px;
		box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
		background: white;
		margin: 2em auto;
	}
	form .location {
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 0.5em;
		position: relative;
		border-radius: 1em 0 0 1em;
	}

	form .location img {
		width: 0.8em;
		height: 0.8em;
	}
	/* search bar */
	input[type='search'] {
		border: 0;
		height: 100%;
		padding: 1em 0;
		width: 100%;
		outline: none;
		background: white;
		border-radius: 0 1.5em 1.5em 0;
	}
	input[type='search']::placeholder {
		color: #222;
		font-size: 1em;
	}

	button {
		border: 0;
		height: 100%;
		width: 100%;
		cursor: pointer;
		border-radius: 0 1.5em 1.5em 0;
		background: #ff4b2b;
		color: white;
		width: 8em;
		padding: 0 0.5em 0 0.5em;
		transition: all 0.5s;
	}
	button:hover {
		opacity: 0.9;
	}

	input[type='search']::-webkit-search-decoration,
	input[type='search']::-webkit-search-cancel-button,
	input[type='search']::-webkit-search-results-button,
	input[type='search']::-webkit-search-results-decoration {
		-webkit-appearance: none;
	}
</style>
