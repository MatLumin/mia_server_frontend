<script>
import {current_surname} from "../stores/current_surname.js";

let {surname} = $props();
let additional_css_class = $state("");
let troubled_class = $state(""); //.reporter_card_troubled on troubled 
let troubled_mark = $state("");

async function the_troubled_mark_things()
{
    let res = await fetch(`http://127.0.0.1:9001/api/reporter/has_any_problem?surname=${surname}`);
    let json = await res.json();
    if (json["data"] == true)
    {
        troubled_class = "reporter_card_troubled";
        troubled_mark = "⚠️"
    }
    troubled_class = "";
    troubled_mark = ""    
}

current_surname.subscribe
(
    async function on_set(value) 
    {
        if (value === surname)
        {
            additional_css_class = "selected_reporter_card"; 
        }
        else 
        {
            additional_css_class = ""
        }
    await the_troubled_mark_things()
    }
    
)


function declare_self_as_selected()
{
    current_surname.set(surname);
}

</script>


<div class="reporter_card {additional_css_class} {troubled_class}" onclick={declare_self_as_selected}>{surname} {troubled_mark}</div>

