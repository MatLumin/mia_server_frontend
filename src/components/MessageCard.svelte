
<script>
let {err_message,
group_username,
hour,
id_of_message,
minute,
second,
sender_phone_number,
was_ok} = $props()
</script>



<div class="message_card general_border secondry_divs_colors general_padding_and_margin scaleup_on_hover">
    message {id_of_message}
    by {sender_phone_number}
    to {group_username}
    failed cause 
    {err_message}
    at {hour}:{minute}:{second}

   
</div>