<template>
	<div class="addTask">
		<input type="text" v-model="task.name">
		<button  v-on:click="addTask()" :class="[task.name ? 'active': 'inacitve']">
			<font-awesome-icon icon="plus-square" />
		</button>
	</div>
</template>

<script>
	export default {
		name: "AddTask",
		data () {
			return {
				task:{
					name: ''
				}
			}
		},
		methods: {
			addTask() {
				// Add new task
				if (this.task.name == '') {
					return;
				}

				axios.post('/api/task/store', {
					task: {
						name: this.task.name
					}
				})
				.then( res => this.task.name = '')
				.catch(err => console.error(err));

				this.$emit('add-task');
			}
		}
	};
</script>