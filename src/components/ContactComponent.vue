
<template>

	<div class="container-fluid px-0" id="contact">
	  <div class="row g-0 align-items-stretch"> 
	    <!-- Google Map -->
	    <div class="col-sm-12 col-md-6 d-flex">
	      <div class="map-container flex-grow-1 my-auto ms-4">
	        <iframe 
	          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d247074.61382048432!2d121.0657695977028!3d14.625212967586874!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3397935fd15b9eb5%3A0x8688b93161d82f9e!2sTanay%2C%20Rizal!5e0!3m2!1sen!2sph!4v1759248067029!5m2!1sen!2sph"
	          allowfullscreen="" 
	          loading="lazy" 
	          referrerpolicy="no-referrer-when-downgrade">
	        </iframe>  
	      </div>
	    </div>

	    <!-- Contact Form -->

	    <div class="col-sm-12 col-md-6 px-5 d-flex align-items-center">
	      <div class="w-100">
	        <div id="contact-title" class="mt-5">
	          <h2 class="mb-5">Contact Us</h2>
	          <p>Let’s connect.</p>
	        </div>
	        <form action="">
	          <div class="mb-3" id="name">
	            <label for="name" class="form-label">Name</label>
	            <input type="text" class="form-control bg-white" id="name" placeholder="Your name"/>
	          </div>
	          <div class="mb-3" id="email">
	            <label for="email" class="form-label">Email address</label>
	            <input type="email" class="form-control bg-white" id="email" placeholder="me@email.com"/>
	          </div>
	          <div class="mb-3" id="message">
	            <label for="message" class="form-label">Message</label>
	            <textarea class="form-control bg-white" id="message" rows="6"></textarea>
	          </div>
	          <button type="button" class="mb-3" id="button">Submit</button>
	        </form>
	      </div>
	    </div>
	  </div>
	</div>
	
</template>