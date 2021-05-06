<script>
    import { createEventDispatcher } from 'svelte';
    import TextInput from '../UI/TextInput.svelte';
    import Modalform from './Modalform.svelte';
    import Button from '../UI/Button.svelte';
	import { isEmpty, isValidEmail } from "../helpers/validation.js";

    let title = "";
	let titleValid = false;
	let subtitle ="";
	let subtitleValid = false;
	let description = "";
	let descriptionValid = false;
	let imageUrl = "";
	let imageUrlValid = false;
	let address = "";
	let addressValid = false;
	let contactEmail = "";
	let contactEmailValid = false;
	let formIsValid = false;
    let showModal = false;

    const dispatch = createEventDispatcher();

	$: formIsValid = !isEmpty(title);
	$: subtitleValid = !isEmpty(subtitle);
	$: descriptionValid = !isEmpty(description);
	$: imageUrlValid = !isEmpty(imageUrl);
	$: addressValid = !isEmpty(address);
	$: contactEmailValid = isValidEmail(contactEmail);

	$: formIsValid = 
			formIsValid && 
			subtitleValid && 
			descriptionValid && 
			imageUrlValid && 
			addressValid && 
			contactEmailValid;


    function submitForm(){
        dispatch('save', {
            title:title,
            subtitle:subtitle,
            description:description,
            imageUrl:imageUrl,
            address:address,
            contactEmail:contactEmail
        });

    }

</script>

<div id="showM"><button on:click="{() => showModal = true }">Show Modal</button></div>

{#if showModal }
<Modalform on:cancel="{() => showModal = false }" on:close="{() => showModal = false }" >
	<h1 slot="header">ADD CONTENT</h1>
	<form on:submit|preventDefault={submitForm} >

		<TextInput 
			id="title" 
			label="Title" 
			type="text"
			valid={titleValid}
			validityMessage="Enter a valid title!"
			value={title} 
			on:input={ event => (title = event.target.value)} 
		/>
		<TextInput 
			id="subtitle" 
			label="SubTitle"
			type="text" 
			valid={subtitleValid}
			validityMessage="Enter a valid subtitle!"
			value={subtitle} 
			on:input={ event => (subtitle = event.target.value)} 
		/>
		<TextInput 
			id="address" 
			label="Address"
			type="text" 
			valid={addressValid}
			validityMessage="Enter a valid address!"
			value={address} 
			on:input={ event => (address = event.target.value)} 
		/>
		<TextInput 
			id="imageurl" 
			label="Image URL"
			type="text" 
			valid={imageUrlValid}
			validityMessage="Enter a valid Image URL!"
			value={imageUrl} 
			on:input={ event => (imageUrl = event.target.value)} 
		/>
		<TextInput 
			id="email" 
			label="E-mail"
			type="email" 
			valid={contactEmailValid}
			validityMessage="Enter a valid E-mail!"
			value={contactEmail} 
			on:input={ event => (contactEmail = event.target.value)} 
		/>
		<TextInput 
			id="description" 
			label="Description"
			controlType="textarea" 
			valid={descriptionValid}
			validityMessage="Enter a valid Description!"
			value={description} 
			on:input={ event => (description = event.target.value)} 
		/>
	
			<Button type="submit" caption="Save" slot="footer" disabled={!formIsValid} />
			<!-- <Button type="button" caption="Close" slot="footer" on:click="{() => showModal = false }" /> -->
			<button on:click="{() => showModal = false }" >Close</button>
	
	</form>
</Modalform>
{/if}

<style>
    form{
		width: 30rem;
		max-width: 90%;
		margin: auto;
	}
    #showM{
		margin-top: 5rem;
		display: flex;
		justify-content: center;
		align-items: center;
	}
</style>