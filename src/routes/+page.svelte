<script>
	let form = {
		firstName: '',
		lastName: '',
		mail: '',
		message: '',
		queryType: '',
		consent: false
	};

	let errors = {
		firstName: false,
		lastName: false,
		mail: false,
		queryType: false,
		message: false,
		consent: false
	};

	let successMessage = false;

	const validateForm = () => {
		let hasErrors = false;

		errors.firstName = !form.firstName.trim();
		errors.lastName = !form.lastName.trim();
		errors.mail = !form.mail.trim() || !form.mail.includes('@');
		errors.message = !form.message.trim();
		errors.queryType = !form.queryType;
		errors.consent = !form.consent;

		hasErrors =
			errors.firstName ||
			errors.lastName ||
			errors.mail ||
			errors.message ||
			errors.queryType ||
			errors.consent;

		successMessage = !hasErrors;
	};

	const submitForm = (e) => {
		e.preventDefault();
		validateForm();

		if (successMessage) {
			form = {
				firstName: '',
				lastName: '',
				mail: '',
				message: '',
				queryType: '',
				consent: false
			};

			setTimeout(() => {
				successMessage = false;
			}, 5000);
		}
	};
</script>

<main class="font-karla text-dark-gray flex items-center justify-center bg-[#E1F1E7]">
	<div class="relative mb-20 mt-20 w-full max-w-lg rounded-lg bg-white p-10 shadow-md">
		{#if successMessage}
			<div class="absolute inset-0 flex items-center justify-center rounded-lg bg-black/50">
				<div class="w-96 rounded-md bg-[#2A4244] p-6 text-center text-white shadow-lg">
					<span
						class="mb-3 inline-block h-8 w-8 items-center justify-center rounded-full bg-green-500 text-xl font-bold text-white"
						>✔</span
					>
					<h2 class="text-lg font-bold">Message Sent!</h2>
					<p>Thanks for completing the form. We'll be in touch soon!</p>
				</div>
			</div>
		{/if}

		<form class="space-y-6" on:submit={submitForm}>
			<h1 class="text-2xl font-bold">Contact Us</h1>

			<!-- First and Last Name -->
			<div class="grid grid-cols-1 gap-4 md:grid-cols-2">
				<label class="flex flex-col">
					<span class="mb-2">First Name <span class="text-green-500">*</span></span>
					<input
						type="text"
						bind:value={form.firstName}
						class="rounded-md border p-2 {errors.firstName ? 'error' : ''}"
					/>
					{#if errors.firstName}
						<span class="text-sm text-red-500">This field is required</span>
					{/if}
				</label>
				<label class="flex flex-col">
					<span class="mb-2">Last Name <span class="text-green-500">*</span></span>
					<input
						type="text"
						bind:value={form.lastName}
						class="rounded-md border p-2 {errors.lastName ? 'error' : ''}"
					/>
					{#if errors.lastName}
						<span class="text-sm text-red-500">This field is required</span>
					{/if}
				</label>
			</div>

			<!-- Email Address -->
			<label class="flex flex-col">
				<span class="mb-2">Email Address <span class="text-green-500">*</span></span>
				<input
					type="text"
					bind:value={form.mail}
					class="rounded-md border p-2 {errors.mail ? 'error' : ''}"
				/>
				{#if errors.mail}
					<span class="text-sm text-red-500">Please enter a valid email address</span>
				{/if}
			</label>

			<!-- Query Type -->
			<label class="flex flex-col">
				<span class="mb-2">Query Type <span class="text-green-500">*</span></span>
				<div class="flex space-x-4">
					<label class="flex items-center space-x-2">
						<input type="radio" bind:group={form.queryType} value="general" class="hidden" />
						<div
							class="flex h-5 w-5 items-center justify-center rounded-full border {form.queryType ===
							'general'
								? 'bg-[#057C62]'
								: ''}"
						></div>
						<span>General Enquiry</span>
					</label>

					<label class="flex items-center space-x-2">
						<input type="radio" bind:group={form.queryType} value="support" class="hidden" />
						<div
							class="flex h-5 w-5 items-center justify-center rounded-full border {form.queryType ===
							'support'
								? 'bg-[#057C62]'
								: ''}"
						></div>
						<span>Support Request</span>
					</label>
				</div>
				{#if errors.queryType}
					<span class="text-sm text-red-500">Please select a query type</span>
				{/if}
			</label>

			<!-- Message -->
			<label class="flex flex-col">
				<span class="mb-2">Message <span class="text-green-500">*</span></span>
				<textarea
					bind:value={form.message}
					class="h-28 rounded-md border p-2 {errors.message ? 'error' : ''}"
				></textarea>
				{#if errors.message}
					<span class="text-sm text-red-500">This field is required</span>
				{/if}
			</label>

			<!-- Consent -->
			<label class="flex items-center space-x-2">
				<input type="checkbox" bind:checked={form.consent} class="hidden" />
				<div
					class="flex h-5 w-5 items-center justify-center rounded-full border {form.consent
						? 'bg-[#057C62]'
						: ''}"
				></div>
				<span>I consent to being contacted by the team <span class="text-green-500">*</span></span>
			</label>
			{#if errors.consent}
				<span class="text-sm text-red-500">Please provide your consent</span>
			{/if}

			<!-- Submit Button -->
			<button
				type="submit"
				class="w-full rounded-md bg-[#0C7D69] py-2 text-white transition hover:bg-green-600"
			>
				Submit
			</button>
		</form>
	</div>
</main>

<style>
	.error {
		border-color: red;
	}

	.absolute {
		z-index: 50;
	}

	.bg-black\/50 {
		background-color: rgba(0, 0, 0, 0.5);
	}
</style>
