<script>
    export let type;
    export let caption;
    export let disabled = false;
</script>

<button type="{type}" on:click {disabled} >{caption}</button>

<style>
    /* a:hover,
    a:active {
        background: #e40763;
        border-color: #e40763;
        box-shadow: 1px 1px 8px rgba(0,0,0,0.26);
    } */
    button:disabled,
    button:disabled:hover,
    button:disabled:active {
        background: #ccc;
        border-color: #ccc;
        color: #959595;
        box-shadow: none;
        cursor: not-allowed;
    }


</style>