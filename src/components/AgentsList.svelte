<script>
import { onMount } from "svelte";
import {current_surname} from "../stores/current_surname.js";
import AgentCard from "./AgentCard.svelte";


let data = $state([]);
let is_mounted = false; 

current_surname.subscribe
(
    async function(new_surname)
    {
        if (is_mounted === false)
        {
            return 
        }
        let res = await fetch(`http://127.0.0.1:9001/api/reporter/get_agents_brief_info?surname=${new_surname}`);
        let json = await res.json();
        data = json["data"];
    }
)

onMount
(
    function()
    {
        is_mounted = true;
    }
)


</script>


<div class="scroll_on_y max_height_screen agents_list major_divs_animation major_divs_color flex_col general_border major_divs_padding_and_margin">
    {#each data as agent_data }
        <AgentCard
        owner_surname={agent_data["owner_surname"]}
        phone_number={agent_data["phone_number"]}
        state_of_now={agent_data["state_of_now"]}
        flood_wait_value={agent_data["flood_wait_value"]}
        message_portion={agent_data["message_portion"]}
        group_portion={agent_data["group_portion"]}
        current_message_id={agent_data["current_message_id"]}
        current_group_username={agent_data["current_group_username"]}
        ></AgentCard>
    {/each}
</div>