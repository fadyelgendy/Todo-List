<template>
	<div>
		<div v-for="(task, index) in tasks" :key="index">
			<Task :task="task" @delete-task="$emit('delete-task')"/>
		</div>
	</div>
</template>

<script>
	import Task from "./Task.vue"

	export default {
		name: "Tasks",
		props: ['tasks'],
		components: {
			Task
		},
	};

</script>