<template>
	<section id="contact" class="p-3">
		<h2 class="text-center pb-2">Contact</h2>
		<div class="row">
			<div class="col-12 col-md-6 d-flex justify-content-md-end mb-3">
				<iframe class="p-3 w-75 mx-auto mx-md-0" src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3860.4100410550705!2d121.0411029757416!3d14.63265027628985!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3397b7f5db7f5e3f%3A0xe15d2d6a4453ed00!2sZuitt%20QC!5e0!3m2!1sen!2sph!4v1759134365240!5m2!1sen!2sph" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
			</div>

			<div class="col-12 col-md-6">
				<form class="bg-none p-3 rounded justify-content-start pe-md-5 w-75 mx-auto mx-md-0" @submit.prevent="submitForm">
					<div class="form-group mb-2">
						<label class="text-dark" for="name">Name</label>
						<input type="text" class="form-control" id="name" placeholder="First Name M.I. Last Name">
					</div>
					<div class="form-group mb-2">
						<label class="text-dark" for="email">Email address</label>
						<input type="email" class="form-control" id="email" placeholder="Email">
	                </div>
	                <div class="form-group mb-2">
	                    <label class="text-dark" for="message">Message</label>
	                    <textarea class="form-control" id="message" rows="7" placeholder="Message"></textarea>
	                </div>
	                <div class="d-flex flex-column flex-md-row justify-content-between align-items-center p-2">
	                    <div class="d-flex gap-3 align-items-center order-2 order-m-1 p-2">
	                    	<a href="https://www.linkedin.com/" target="_blank"><img class="linkedin-img img-fluid justify-content-center" src="./images/linkedin-logo.png"></a>
	                    	<a href="https://www.kalibrr.com/home" target="_blank"><img class="kalibrr-img img-fluid justify-content-center" src="https://upload.wikimedia.org/wikipedia/commons/8/8a/Kalibrr_Logo.png"></a>
	                    	<a href="https://ph.indeed.com/?r=us" target="_blank"><img class="indeed-img img-fluid justify-content-center" src="https://1000logos.net/wp-content/uploads/2023/01/Indeed-Logo-2004.png"></a>
	                    </div>
	                    <button type="button" class="btn btn-dark p-2 order-1 order-md-2" data-bs-toggle="modal" data-bs-target="#thanksModal">Send Email</button>

	                    <div class="modal" id="thanksModal" tabindex="-1">
				  			<div class="modal-dialog">
				    			<div class="modal-content">
				      				<div class="modal-header">
				        				<h5 class="modal-title">Thank you for sending an email!</h5>
				        				<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
				      				</div>
				      				<div class="modal-body">
				        				<p>I will respond to you soon.</p>
				      				</div>
					      			<div class="modal-footer">
					        			<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
					      			</div>
					    		</div>
					  		</div>
						</div>
	                </div>
	            </form>
			</div>
		</div>
	</section>
</template>

<script setup>
	import { ref } from 'vue';
	import { Notyf } from 'notyf';
	import 'notyf/notyf.min.css';

	const notyf = new Notyf();

	const WEB3FORMS_ACCESS_KEY = "ddb1167c-a013-45d5-859b-5edd5139113b";

	const subject = "New message from Portfolio Contact Form";

	const name = ref("");
	const email = ref("");
	const message = ref("");

	const isLoading = ref(false);

	const submitForm = async() => {

		isLoading.value = true;

		try {
			const response = await fetch("https://api.web3forms.com/submit", {
				method: 'POST',
				headers: {
					"Content-Type": "application/json",
					Accept: "application/json",
				},
				body: JSON.stringify({
					access_key: WEB3FORMS_ACCESS_KEY,
					subject: subject,
					name: name.value,
					email: email.value,
					message: message.value
				})
			})

			const result = await response.json();

			if(result.success)
			{
				console.log(result);
				isLoading.value = false;
				notyf.success("Message sent!");
			}
		}
		catch(error){
			console.log(error);
			isLoading.value = false;
			notyf.error("Failed to send message.");
		}
	}
</script>