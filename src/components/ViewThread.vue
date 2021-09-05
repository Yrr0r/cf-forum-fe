<template>
	<div class="block">
		<h1 class="title">ThreadView</h1>
		<code>{{this.nodeid}}</code>
		<h1 v-if="loading">Loading</h1>
		<div v-else>
			<div class="block" v-for="(value, name) in this.node" v-bind:key="name">
				<div class="card">
					<div class="card-header">
						<p class="card-header-title"> {{name}} </p>
					</div>
					<div class="card-content">
						{{value}}
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'ViewThread',
	props: ['nodeid'],
	data() {return {
		loading: true,
		node: {},
	}},
	created(){
		this.fetchNode();
	},
	methods: {
		async fetchNode(){
			// todo: get permcode from storage
			let reqParam = {
				method: 'read',
				threadId: this.nodeid.nodeId
			}
			let response = await fetch('/api/discuss', {
				method: 'POST',
				body: JSON.stringify(reqParam)
			})
			let result = await response.json()
			this.loading = false;
			this.node = result;
			console.log(this.node);
		}
	}
}
</script>