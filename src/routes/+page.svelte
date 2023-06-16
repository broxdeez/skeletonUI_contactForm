<script>
	import { localStorageStore } from '@skeletonlabs/skeleton';

	const contactStore = localStorageStore('contactStore', []);
	let inputName = '';
	let inputPhno = '';

	function addContact() {
		$contactStore = [
			{
				name: inputName,
				phoneNumber: inputPhno
			},
			...$contactStore
		];

		inputName = '';
		inputPhno = '';
	}

	function deleteContact(index) {
		$contactStore = $contactStore.filter((contact, contactIndex) => contactIndex !== index)
	}
</script>

<div class='flex justify-end p-8'>
	<a href="https://github.com/broxdeez/skeletonUI_contactForm">
		<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-github"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
	</a>
</div>

<div class="container h-full mx-auto flex flex-col justify-center items-center">
	<div class="card sm:w-1/2 p-10 space-y-5 flex flex-col">
		<h1 class="h1">Contact Form</h1>
		<p>Enter details below to save contact info</p>
		<div class="space-y-2">
			<label for="Name" class="label ml-2">Name</label>
			<input id="Name" type="text" class="input w-4/5" bind:value={inputName} />
			<label for="Phone" class="label ml-2">Phone Number</label>
			<input id="Phone" type="text" class="input w-4/5" bind:value={inputPhno} />
		</div>
		<button class="btn variant-filled-primary w-fit px-5" on:click={addContact}> Submit </button>
	</div>

	<div class="card sm:w-1/2 p-8 space-y-5 flex flex-col mt-10">
		<h2 class="h2">Stored Contacts</h2>
		{#each $contactStore as contact, index}
			<div class="card p-4 ">
				<h4 class="h4">Name : {contact.name}</h4>
				<h4 class="h4">Phone Number : {contact.phoneNumber}</h4>
				<button class="btn variant-filled-secondary mt-4" on:click={() => deleteContact(index)}>Delete</button>
			</div>
		{/each}
	</div>
</div>
