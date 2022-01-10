<template>

<div id="app">
	<h1>Your To Do List (VUE3)</h1>
	<formSubmit @add:todo="addToDo"/>
	<table id="todoTable">
		<tr class="todoitem" v-for="(todo,index) in todolist" :key="index">
			<td class="indexCell" >{{index+1}}.</td>
			<td v-if="editing === index">
				<input class="editInPlaceCell" type="text" v-model="todolist[index]" />
			</td>
			<td class="todoContentCell" v-else>{{todo}}</td>
			<td v-if="editing === index">
				<button @click="editing=null">Save</button>
				<button class="muted-button" @click="cancelEditing(index)">Cancel</button>
			</td>
			<td v-else>
				<button @click="editMode(index)">Edit</button>
				<button @click="deleteToDo(index)"  >Delete</button>
			</td>
		</tr>
	</table>
</div>

</template>

<script>
import formSubmit from './components/formSubmit.vue'

export default {
	name: 'App',
	components: {    formSubmit  },
	data(){
		return {
			todolist:[],
			editing: null,
			oldToDoContent: "",
		};
	},
	methods: {
		addToDo(todo){
			this.todolist=[todo, ...this.todolist]
		},
		deleteToDo(index){
			this.todolist.splice(index,1);
		},
		editMode(index) {
			this.oldToDoContent=this.todolist[index];
			this.editing = index;
		},
		cancelEditing(index) {
			this.todolist[index]=this.oldToDoContent;
			this.editing = null;
		}
	},
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: auto;
  margin-top: 60px;
  width:600px;

}

#todoTable{
	margin-left: 55px;
	margin-top:  20px;
}
.todoitem{
	text-align:left;
	
}

.indexCell{
	width: 30px;
}
.todoContentCell{
	width: 300px;
}
.editInPlaceCell{
	width: 280px;
}

</style>
