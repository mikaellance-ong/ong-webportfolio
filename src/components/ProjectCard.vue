<template>
	<div class="col-12 col-md-3 pb-5 d-flex justify-content-center">
		<div class="card h-100">
			<img :src="project.image" class="card-img-top img-fluid p-3">
			<div class="card-body">
				<h5 class="card-title">{{ project.title }}</h5>
		    	<p class="card-text py-2">{{ project.description }}</p>
		  	</div>
		</div>
	</div>
</template>

<script setup>
	import { defineProps } from 'vue';

	defineProps({
		project: Object
	})
</script>