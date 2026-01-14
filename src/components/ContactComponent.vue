<script setup>
import { ref, onMounted } from "vue";
import {Notyf} from "notyf"

const WEB3FORMS_ACCESS_KEY = "632030ee-135e-46c2-9a49-99df3dcbe05a";
const subject = ref("New Contact from Portfolio")
const name = ref("")
const email = ref("")
const message = ref("")

const isLoading = ref(false)

const notyf = new Notyf();

// configurations needed for recaptcha
const SITE_KEY="6LfiEUosAAAAAJbtYg5QjATsZPhzyVCp1GzsbQj3";
const recaptchaContainer = ref(null);
const recaptchaWidgetId = ref(null);
const recaptchaToken = ref('');

	// Callback called by reCAPTCHA when successful
function onRecaptchaSuccess(token) {
  recaptchaToken.value = token;
}

// Callback when expired
function onRecaptchaExpired() {
  recaptchaToken.value = '';
}

// Function to render the reCAPTCHA widget
function renderRecaptcha() {
  if (!window.grecaptcha) {
    console.error('reCAPTCHA not loaded');
    return;
  }

  recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
    sitekey: SITE_KEY,
    size: 'normal', // or 'compact'
    callback: onRecaptchaSuccess,
    'expired-callback': onRecaptchaExpired,
  });
}

// Function to reset reCAPTCHA 
function resetRecaptcha() {
  if (recaptchaWidgetId.value !== null) {
    window.grecaptcha.reset(recaptchaWidgetId.value);
    recaptchaToken.value = '';
  }
}


onMounted(() => {
  // This code waits for the Google reCAPTCHA library to load, then renders the reCAPTCHA widget using onMounted hook. 
  // The widget is rendered with grecaptcha.render(), which requires a sitekey. 
  // Callback functions handle success and expiration events. 
  // reCAPTCHA is reset upon form submission to clear the token.
  const interval = setInterval(() => {
    if (window.grecaptcha && window.grecaptcha.render) {
      renderRecaptcha();
      clearInterval(interval);
    }
  }, 100);

  onBeforeUnmount(() => {
    clearInterval(interval);
  });
});

const submitForm = async () => {

	if(!recaptchaToken.value){
		notyf.error("Please verify that you are not a robot!");
		return
	}

	isLoading.value = true;
	try {

  	const response = await fetch("https://api.web3forms.com/submit", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
    },
    body: JSON.stringify({
      access_key: WEB3FORMS_ACCESS_KEY,
      subject: subject.value,
      name: name.value,
      email: email.value,
      message: message.value,
    }),
  });

  const result = await response.json();

  if (result.success) {
    console.log(result);
    isLoading.value = false;
    notyf.success("Message Success!")

    name.value = ""
    email.value = ""
    message.value = ""
  }

  }catch(error){

  	console.log(error)

  	isLoading.value = false;
  	notyf.error("Failed to send a message.")
	}
}

</script>


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

	        <form @submit.prevent="submitForm">

	          <div class="mb-3" id="name">
	            <label for="name" class="form-label">Name</label>
	            <input v-model="name" type="text" class="form-control bg-white" id="name" placeholder="Your name" required />
	          </div>
	          <div class="mb-3" id="email">
	            <label for="email" class="form-label" required>Email address</label> 
	            <input v-model="email" type="email" class="form-control bg-white" id="email" placeholder="me@email.com" required />
	          </div>
	          <div class="mb-3" id="message">
	            <label for="message" class="form-label" required>Message</label>
	            <textarea v-model="message" class="form-control bg-white" id="message" rows="6" required></textarea>
	          </div>

	          <button type="submit" class="submit-btn pl-5 pr-5 mb-3" id="button" :disabled="isLoading" >{{isLoading ? "Sending..." : "Submit"}}</button>

		      <div class="d-flex justify-content-end mt-2">
	            <div ref="recaptchaContainer"></div>
	          </div>

	        </form>

	      </div>
	    </div>
	  </div>
	</div>
	
</template>