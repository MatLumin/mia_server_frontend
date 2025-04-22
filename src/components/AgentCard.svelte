<script>

let {owner_surname,phone_number,state_of_now,flood_wait_value,message_portion,group_portion,current_message_id,current_group_username} = $props();

</script>


<div class="general_border secondry_divs_colors general_padding_and_margin agent_card scaleup_on_hover ">
owner_surname = {owner_surname}
phone = {phone_number}
c message = {current_message_id}
c group = {current_group_username}
state = {state_of_now}
flood wait = {flood_wait_value}
message portion = {message_portion}
group portion = {group_portion}
</div>