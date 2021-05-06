<script>
	import Header from './UI/Header.svelte';
	import Meetupgrid from './Meetups/Meetupgrid.svelte';
	import TextInput from './UI/TextInput.svelte';
	import Button from './UI/Button.svelte';
	import Modalform from './Meetups/Modalform.svelte';
	import Meetupitem from './Meetups/Meetupitem.svelte';
	import EditMeetups from './Meetups/EditMeetups.svelte';


	
	
	let meetups = [
		{
			id: 'm1',
			title: 'Coding Bootcamp',
			subtitle: 'Learn to code in comfirt hours',
			description: 'In this meetups , we will have some experts that teach you',
			imageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQq_NoFnfBJU3lwVyfJwdQCf3wjnj-SyuvxpA&usqp=CAU',
			address: 'Cantt Kanpur',
			contactEmail: 'asif.hell111@gmail.com',
			isFavorite: false
		},
		{
			id: 'm2',
			title: 'Swim Together',
			subtitle: 'Let\'s go for some swimming ',
			description: 'We will simply swim some rounds!',
			imageUrl: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTaKOfLXD_vKZroriMr0twh3rhlGroUaZzh8Q&usqp=CAU',
			address: 'Cantt Kanpur',
			contactEmail: 'asif.hell@gmail.com',
			isFavorite: false
		}
	];

	let editMode = null;

	//Adding new meetup using add new array

	function addMeetup(event){
		let newMeetup = {
			id: Math.random().toString(),
			title: event.detail.title,
			subtitle: event.detail.subtitle,
			description: event.detail.description,
			imageUrl: event.detail.imageUrl,
			address: event.detail.address,
			contactEmail: event.detail.contactEmail
		};

		// meetups.push(newMeetup); // Does not work

		meetups = [newMeetup, ...meetups];

		editMode = null;

	}

	function toggleFavorite(event){

		const id = event.detail;
		const updatedMeetup = { ...meetups.find(m => m.id === id) };
		updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
		const meetupIndex = meetups.findIndex(m => m.id === id );
		const updatedMeetups = [...meetups];
		updatedMeetups[meetupIndex] = updatedMeetup;
		meetups = updatedMeetups;

	}

</script>

<Header />

<main>
	<div class="new-meetup"></div>
	<Button caption="New Meetups" on:click={() => editMode = 'add' } />
		{#if editMode === 'add' }
			<EditMeetups on:save={addMeetup} />
		{/if}
	<Meetupgrid {meetups} on:togglefavorite="{toggleFavorite}" />
</main>

<style>
	.new-meetup{
		margin: 1rem;
	}
	main {
		margin-top: 5rem;
	}
</style>