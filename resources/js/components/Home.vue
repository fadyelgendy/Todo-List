<template>
	<div>
		<Header />
			<div class="container">
				<AddTask @add-task="addTask" />
				<Tasks :tasks="tasks" @delete-task="deleteTask" />
			</div>
		<Footer />
	</div>
</template>

<script>
import Header from "./inc/Header.vue"
import Footer from "./inc/Footer.vue"
import Tasks from "./Tasks.vue"
import AddTask from "./AddTask.vue"

	export default {
		name: "Home",
		components: {
			Header,
			Footer,
			Tasks,
			AddTask
		},
		data () {
			return {
				tasks:[]
			}
		},
		methods:{
			getList() {
				axios.get('/api/tasks')
				.then(res => {this.tasks = res.data})
				.catch(err => console.error(err));
			},
			addTask (){
				this.getList();
			},
			deleteTask () {
				this.getList();
			}
		},
		created() {
			this.getList();
		}
	};

</script>