<template>
	<h2>Users</h2>

	<UserObject v-for="user in users" :key="user.id" :user="user" />
</template>
<script>
import axios from 'axios';
import { defineAsyncComponent, ref } from 'vue';

// import UserObject from './UserObject';
const UserObject = defineAsyncComponent(() =>
	import('./UserObject' /*webpackChunkName:"user" */)
);

export default {
	components: {
		UserObject,
	},
	async setup() {
		const users = ref(null);

		const response = await axios.get(
			'https://jsonplaceholder.typicode.com/users'
		);
		users.value = response.data;
		return {
			users,
		};
	},
};
</script>

<style></style>
