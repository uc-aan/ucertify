<script>
    export let controlType;
    export let id;
    export let label;
    export let rows;
    export let value;
    export let type;
    export let valid = true;
    export let validityMessage = '';
    let touched = false;
</script>

<div class="form-control">
    <label for="{id}">{label}</label>
    {#if controlType === 'textarea'}
        <textarea class:invalid="{!valid && touched}" rows="{rows}" id="{id}" value={value} on:input
         on:blur="{ () => touched = true }" />
    {:else}
        <input type="{type}" class:invalid="{!valid && touched}" id="{id}" value={value} on:input 
        on:blur="{ () => touched = true }" />
    {/if}

    {#if validityMessage && !valid && touched }
        <p class="error-message">{validityMessage}</p>
    {/if}
</div>

<style>
    textarea,
    input{
        width: 100%;
        border-top: none;
        border-left: none;
        border-right: none;
        border-bottom: 2px solid black;
    }
    textarea:hover{
        border-bottom: 2px solid red;
    }
    input:hover{
        border-bottom: 2px solid red;
    }
    label {
        display: block;
        margin-bottom: 0.5rem;
        width: 100%;
    }
    .form-control {
        padding: 0.5rem 0;
        width: 100%;
        margin: 0.25rem 0;
    }
    .invalid {
        border-color: red;
        background-color: rgb(250, 191, 191);
    }
    .error-message {
        color: red;
        margin: 0.25rem 0;
    }
</style>