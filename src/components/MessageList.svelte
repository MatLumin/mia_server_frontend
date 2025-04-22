<script>
import { onMount } from "svelte";
import MessageCard from "./MessageCard.svelte";
import {current_surname} from "../stores/current_surname.js";
current_surname.subscribe


let troubled_messages = $state(null);
let current_surname_value = "";

current_surname.subscribe(
    async function(new_surname)
    {
        current_surname_value = new_surname
    }
)




onMount
(
    function() 
    {
        setInterval
        (
            async function () 
            {
                let url = `http://127.0.0.1:9001//api/reporter/get_problems_in_sending?surname=${current_surname_value}`;
                let res = await fetch(url);
                let json = await res.json();
                troubled_messages = json["data"];
            }
            ,1000
        );
    }
)

</script>


<div class="scroll_on_y max_height_screen message_list major_divs_animation major_divs_color flex_col major_divs_padding_and_margin">
    {#each troubled_messages as troubled_message}
        <MessageCard
        err_message={troubled_message["err_message"]}
        group_username={troubled_message["group_username"]}
        hour={troubled_message["hour"]}
        id_of_message={troubled_message["id_of_message"]}
        minute={troubled_message["minute"]}
        second={troubled_message["second"]}
        sender_phone_number={troubled_message["sender_phone_number"]}
        was_ok={troubled_message["was_ok"]}
        ></MessageCard>
    {/each}


</div>