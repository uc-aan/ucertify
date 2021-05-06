<script>
    import { createEventDispatcher } from 'svelte';
    import { fade, fly, scale } from 'svelte/transition';

    const dispatch = createEventDispatcher();
</script>

<div transition:fade class="backdrop" on:click="{() => dispatch('cancel') }" />
<div transition:fly={{ y: 300 }} class="model">
    <header class="header">
        <slot name="header" />
    </header>
    <slot />
    <footer>
        <slot name="footer"/>
            <!-- <button on:click="{() => dispatch('close') }" >Close</button> -->
    </footer>
</div>

<style>
    *{
        font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    }
    .header {
        border-bottom: 1px solid red;
        text-align: center;
    }
    .backdrop {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        background: rgba(0,0,0,0.8);
        z-index: 10;
    }
    .model {
        padding: 1rem;
        position: fixed;
        top: 10vh;
        left: 30%;
        width: 40%;
        height: 70vh;
        background: white;
        border-radius: 5px;
        z-index: 100;
        box-shadow: 0 2px 8px rgba(0,0,0,0.26);
        overflow: scroll;
    }
</style>