
<script setup>
	import {defineProps} from 'vue';

	defineProps({
		project: Object
	})

</script>


<template>
	
	<div class="col-md-3">
	    <div class="project-card h-100">
	      <div class="screenshot">
	        <img :src="project.image" width="200" class="img-fluid ps-4 pt-5">
	      </div>
	      <h3>{{project.title}}</h3>
	      <p>
	      	{{project.description}}
	      </p>
	    </div>
	</div>

</template>