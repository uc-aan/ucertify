<script>
    import Meetupitem from './Meetupitem.svelte';

    export let meetups;
</script>

<section class="meetups">
    {#each meetups as meetup }
        <Meetupitem 
            id={meetup.id}
            title={meetup.title} 
            subtitle={meetup.subtitle} 
            description={meetup.description} 
            imageUrl={meetup.imageUrl}
            address={meetup.address}
            contactEmail={meetups.contactEmail}
            isFav={meetup.isFavorite}
            on:togglefavorite
        />
    {/each}
</section>


<style>
    section {
        width: 100%;
        display: grid;
        grid-template-columns: 1fr;
        grid-gap: 1rem;
    }

    @media (min-width: 640px){
        section {
            grid-template-columns: repeat(2, 1fr);
        }
    }
</style>