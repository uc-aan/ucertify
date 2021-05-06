<script>
    import { scale } from 'svelte/transition';
    import Button from '../UI/Button.svelte';
    import { createEventDispatcher } from 'svelte';
    import Badge from '../UI/Badge.svelte';

    export let id;
    export let title;
    export let subtitle;
    export let description;
    export let imageUrl;
    export let address;
    export let contactEmail;
    export let isFav;

    const dispatch = createEventDispatcher();

</script>

<article transition:scale>
    <header>
        <h1>
            {title}
            {#if isFav}
            <Badge>FAVORITE</Badge>
            {/if}
        </h1>
        <h2>{subtitle}</h2>
        <p>{address}</p>    
    </header>
    <div class="image">
        <img alt="{title}" src="{imageUrl}">
    </div>
    <div class="content">
        <p>{description}</p>
    </div><br />
    <footer>
        <Button href="mailto:{contactEmail}" caption="Contact" />
        <Button type="button" caption="Show Detail" />
        <Button type="button" caption="{isFav ? 'Unfavorite' : 'Favorite'}" on:click="{() => dispatch('togglefavorite',id) }"/>
    </footer>
</article>

<style>
    article{
        padding: 1rem;
        box-shadow: 0 2px 8px rgba(0,0,0,0.26);
        border-radius: 5px;
        background: white;
        margin: 0;
    }
    /* .content {
        
        margin: auto;
        background-color: red;
    } */
    /* header,
    .content,
    footer{
        height: 4rem;
        background-color: rosybrown;
    } */
    /* img {
        width: 300px;
    } */
    .image {
        overflow: hidden;
        width: 100%;
        height: 50%;
        object-fit: cover;
        /* background-color: seagreen; */
    }

    h1 {
        font-size: 1.25rem;
        margin: 0.5rem 0;
        font-family: 'Courier New', Courier, monospace;
    }
    /* h1,is-favorite {
        background: #01a129;
        color: white;
        padding: 0 0.5rem;
        border-radius: 5px;
    } */
    h2 {
        font-size: 1rem;
        color: #808080;
        margin: 0.5rem 0;
    }
    p{
        font-size: 1.25rem;
        margin: 0;
    }
    div {
        text-align: center;
    }
</style>