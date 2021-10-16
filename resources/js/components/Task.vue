<template>
	<div :class="[task.completed ? 'completed' : 'task' , 'task' ]">
		<input type="checkbox" v-model="task.completed" @change="checkComplete">
		<span>{{ task.name }}</span>
		<button class="trash" @click="deleteTask" >
			<font-awesome-icon icon="trash" />
		</button>
	</div>
</template>

<script>
	export default {
		name: "Task",
		props: ['task'],
		methods: {
			checkComplete () {
				axios.put(`/api/task/${this.task.id}`, {
					task: {
						completed: this.task.completed,
						completed_at: Date.now()
					}
				})
				.then(res => console.log(res.data))
				.catch(err => console.error(err));
			},
			deleteTask () {
				axios.delete(`/api/task/${this.task.id}`)
				.then(res => console.log(res.data))
				.catch(err => console.error(err));

				this.$emit('delete-task');
			}
		}
	};
</script>