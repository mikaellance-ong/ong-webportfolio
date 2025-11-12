<template>
	<section id="projects" class="p-4">
		<h2 class="text-center pb-2">My Projects</h2>
		<div v-for="(group, index) in chunkedProjects" :key="index" class="card-deck d-flex flex-wrap gap-2 justify-content-center">
	    	<ProjectCard v-for="project in group" :key="project.id" :project="project" />
	    </div>
	</section>
</template>

<script setup>
	import { computed } from 'vue';
	import ProjectCard from './ProjectCard.vue';
	import projects from '../data/projects.json';

	const chunkSize = 3;

	const chunkedProjects = computed(() => {
		const chunks = [];

		for(let i = 0; i < projects.length; i += chunkSize)
		{
			chunks.push(projects.slice(i, i + chunkSize));
		}

		return chunks;
	})
</script>