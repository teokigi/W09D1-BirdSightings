<template lang="html">
	<form id="sightings-form" v-on:submit.prevent="addSightings" method="post">
		<h2>Add a Sighting</h2>
		<div class="formWrap">
			<label for="species">Species:</label>
			<input type="text" v-model="species"id="species" placeholder="add name of species" required />
		</div>
		<div class="formWrap">
			<label for="location">Location:</label>
			<input type="text" v-model="location"id="location" placeholder="add location" required />
		</div>
		<div class="formWrap">
			<label for="date">Date:</label>
			<input type="date" v-model='date'id="date" required/>
		</div>

		<input type="submit" value="Save" id="save"/>
	</form>
</template>

<script>
import SightingService from '@/services/SightingService.js'
import {eventBus} from "@/main.js"
export default {
	name: 'sightings-form',
	data() {
		return {
		species:'',
		location: '',
		date:""
		}
	},
	methods: {
		addSightings(event){
			const newSightings = {
				species: this.species,
				location: this.location,
				date:this.date
			}
			SightingService.postSightings(newSightings)
			.then(sight => eventBus.$emit("add-sight", sight))
			this.species = this.location = this.date = ""
		}

	}
}
</script>

<style lang="css" scoped>
h2 {
	margin: 10px 0;
	padding: 0;
}

form {
	width: 75%;
	margin: 0 auto;
	background: rgba(255, 255, 255, 0.7);
	padding: 20px;
	margin-bottom: 40px;
}

label {
	min-width: 100px;
	display: inline-block;
}

.formWrap {
	margin-bottom: 10px;
}
</style>
