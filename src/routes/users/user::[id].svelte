<script context="module">
	import { data } from '../../stores';
	export async function load({ params }) {
		let users = [];
		data.forEach((data) => {
			users = data;
		});
		const id = params.id;

		const user = users.find((user) => user.id == id);

		return {
			props: {
				user
			}
		};
	}
</script>

<script>
	export let user;
</script>

<h1>{user.name}</h1>
<p>{user.age}</p>
<p>{user.bio}</p>
<a href="/">Go Back</a>
