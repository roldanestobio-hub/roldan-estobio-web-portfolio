
<script setup>
	import ProjectsCard from './ProjectsCard.vue';
    import projects from '../data/projects.json';
    import {computed} from 'vue';

    const chunkSize = 3;

    const chunkedProject = computed(() => {

        const chunks = [];

        for(let i = 0; i < projects.length; i += chunkSize) {

            chunks.push(projects.slice(i, i + chunkSize));
        }

        return chunks;
    })
	
</script>


<template>
	<!-- MY PROJECTS -->
  	<div class="container-fluid py-5" id="projects">
	    <h2 class="section-title mt-5 text-center">My Projects</h2>
	   	<div
	        v-for="(group, index) in chunkedProject"
	        :key="index"
	        class="row my-4 justify-content-center"
	    >
	    <ProjectsCard 
	        v-for="project in group"
	        :key="project._id"
	        :project="project"
	    />
    	</div>
  	</div>
</template>