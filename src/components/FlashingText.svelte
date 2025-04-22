

<style>
</style>

<script>

let {duration} = $props();
let state_of_now = $state("");

setInterval
(
    function () 
    {
        if (state_of_now == "hidden")
        {
            state_of_now = "visible";
        }
        else 
        {
            state_of_now = "hidden";
        }
    }, duration
)

</script>

<div style="display:inline;">
    {#if state_of_now==="visible"}
    <slot></slot>
    {/if}
</div>