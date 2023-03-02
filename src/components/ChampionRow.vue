<template>
	<tr>
		<td><img v-bind:src="champion['portrait']" v-bind:alt="champion['name']"/></td>
		<td v-bind:class="comparesimple('gender')">{{champion["gender"]}}</td>
		<td v-bind:class="comparearray('ranges')">{{champion["ranges"].join(", ")}}</td>
		<td v-bind:class="comparearray('lanes')">{{champion["lanes"].join(", ")}}</td>
		<td v-bind:class="comparesimple('resource')">{{champion["resource"]}}</td>
		<td v-bind:class="comparearray('regions')">{{champion["regions"].join(", ")}}</td>
		<td v-bind:class="comparearray('species2')">{{champion["species2"].join(", ")}}</td>
		<td v-bind:class="comparedate()"><span v-if="comparedate() != 'bg-success'">{{datearrow() ? "&darr;": "&uarr;"}}</span>{{champion["releaseDate"].split("-")[0]}}</td>
	</tr>
</template>
<script lang="ts">
	export default {
		props: ["selectedchampion", "champion"],
		methods: {
			datearrow(){
				return parseInt(this.champion["releaseDate"].split("-")[0]) > parseInt(this.selectedchampion["releaseDate"].split("-")[0]);
			},
			comparedate(){
				return this.champion["releaseDate"].split("-")[0] == this.selectedchampion["releaseDate"].split("-")[0] ? "bg-success" : "bg-danger";
			},
			comparesimple(property){
				return this.champion[property] === this.selectedchampion[property] ? "bg-success" : "bg-danger";
			},
			comparearray(property){
				if (this.selectedchampion[property].join("") == this.champion[property].join("")){
			      return "bg-success";
			    }else{
			    	var result = "";
			    	var items = this.selectedchampion[property];
			        this.champion[property].forEach(function(item){
			          	if (items.includes(item)) {
			            	result = "bg-warning";
			         	}
			        });
			        if(result!=""){
			        	return result;
			        }
			    }
			    return "bg-danger";
			    
			}
		}

	}
</script>