
<script>
import { onMount } from "svelte";
import ReporterCard from "./ReporterCard.svelte";

let {surname} = $props();
let data = $state([]); // an array of strings


onMount
(
    async function fetch_data()
    {
        let response = await fetch("http://127.0.0.1:9001/api/reporter/get_surnames");
        let json = await response.json();
        data = json["data"]
    }
)

</script>

<div class="scroll_on_y max_height_screen reporters_list major_divs_animation major_divs_color flex_col general_border major_divs_padding_and_margin">
    {#each data as surname}
    <ReporterCard surname="{surname}"></ReporterCard>
    {/each}
        

</div>