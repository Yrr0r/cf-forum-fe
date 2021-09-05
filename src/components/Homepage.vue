<template>
	<div class="block">
		<h1 class="title"> Homepage </h1>
		<div v-if="loading">
			<h1 class="title"> Loading... </h1>
		</div>
		<div v-else>
			<div class="block" v-for="each in mainpage" v-bind:key="each">
				<div class="card">
					<div class="card-header">
						<div class="card-header-title">
							<a v-on:click="$emit('viewThread', each)">{{each["data"]["title"]}}</a>
						</div>
					</div>
					<div class="card-content">
						<code>
							{{JSON.stringify(each)}}
						</code>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "Homepage",
	props:{},
	created(){
		this.getMainPage();
	},
	methods:{
		async getMainPage(){
			let response = await fetch('/api/mainpage',{
				method: 'GET'
			})
			let result = await response.json();
			//console.log("Response: ", response, "Result:", result)
			// filter empty objects:
			for(let each in result){
				if(Object.keys(result[each]).length < 2){
					delete result[each] ;
				}
				if(result[each] == undefined || result[each].data == undefined){
					delete result[each] ;
				}
			}
			this.loading = false;
			this.mainpage = result;
		}
	},
	data(){
		return {
			loading: true,
			mainpage: {}
		}
	}
}
</script>