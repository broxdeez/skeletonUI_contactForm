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
