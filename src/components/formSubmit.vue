<template>
<form @submit.prevent="handleSubmit">
  <input id="inputTODO" v-model="todoContent" type="text" placeholder="what to do next?">
  <input class="btn btn-info" type="submit" value="JustDoIt!">
</form>
</template>
<script>
export default {
	name: 'formSubmit',
	data() {
		return {
			todoContent: ""
		}
	},
	methods: {
		handleSubmit() {
			this.$emit("add:todo", this.todoContent);
			this.todoContent="";
		},
	},
}
</script>
<style scoped>
#inputTODO{
	width:400px;
	height:37px;
	
}

</style>
