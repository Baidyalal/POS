<?php
echo form_open('customers/save/'.$person_info->person_id,array('id'=>'customer_form'));
?>
<div id="required_fields_message"><?php echo $this->lang->line('common_fields_required_message'); ?></div>
<ul id="error_message_box"></ul>
<fieldset id="customer_basic_info">
<legend><?php echo $this->lang->line("customers_basic_information"); ?></legend>
<?php

	$id=$person_info->person_id;
	$title=$person_info->person_title;
	$person_type=$person_info->person_type;

	$sql="select * from ospos_people order by person_id desc limit 0,1";
	$res=mysql_query($sql);
	$row=mysql_fetch_assoc($res);
	$out=$row["person_id"];
	$final_out=$out+1;

?>

<?php if(($id!="") && ($person_type=='2')){ ?>

	<div class="field_row clearfix">

	<?php
	$sel="select * from ospos_customers where person_id='$id'";
	$sel_exe=mysql_query($sel);
	$res_fetch=mysql_fetch_assoc($sel_exe);
	$acnt_num=$res_fetch["account_number"];

	echo form_label($this->lang->line('common_acnt').':', 'common_acnt');
	?>

	<div class='form_field'>

	<?php echo form_input(array(
       		'id'=>'acnt_num',
		'readonly'=>'readonly',
		'value'=>"$acnt_num")
		);
	?>

	</div>

	</div>
<?php }?>

<div class="field_row clearfix">
<?php echo form_label($this->lang->line('common_title').':', 'person_title'); ?>
<?php if($id!="") { ?>
	<?php
	if($person_info->person_title==1){$ti='Mr';}if($person_info->person_title==2){$ti='Mrs';}if($person_info->person_title==3){$ti='M/s';}?>
	<div class='form_field'>
	<?php echo form_dropdown('common_title', array(
	"$person_info->person_title"=>"$ti"), $this->config->item('person_title'))
	?>
	</div>
     	<?php } else { ?>
      	<div class='form_field'>
	<?php echo form_dropdown('common_title', array(
		''	=>'--select--',
		'1'    => 'Mr.',
                '3'    => 'M/s.',
		'2'   => 'Mrs.'), $this->config->item('person_title'));
	?>
	</div>
	<?php }?>
</div>
<div class="field_row clearfix">	
<?php echo form_label($this->lang->line('common_first_name').':', 'first_name',array('class'=>'required')); ?>
	<div class='form_field'>
	<?php echo form_input(array(
		'name'=>'first_name',
		'id'=>'first_name',
		'value'=>$person_info->first_name)
	);?>
	</div>
</div>
<div class="field_row clearfix">


<?php echo form_label($this->lang->line('common_last_name').':', 'last_name',array('class'=>'required')); ?>
	<div class='form_field'>
	<?php echo form_input(array(
		'name'=>'last_name',
		'id'=>'last_name',
		'value'=>$person_info->last_name)
	);?>
	</div>
</div>
<input type="hidden" id="account_number" name="account_number" value="<?php echo $final_out;?>" />

<?php $this->load->view("people/form_basic_info"); ?>
<div class="field_row clearfix">	
<?php echo form_label($this->lang->line('customers_taxable').':', 'taxable'); ?>
	<div class='form_field'>
	<?php echo form_checkbox('taxable', '1', $person_info->taxable == '' ? TRUE : (boolean)$person_info->taxable);?>
	</div>
</div>

<?php
echo form_submit(array(
	'name'=>'submit',
	'id'=>'submit',
	'value'=>$this->lang->line('common_submit'),
	'class'=>'submit_button float_right')
);
?>
</fieldset>
<?php
echo form_close();
?>
<script type='text/javascript'>

//validation and submit handling
$(document).ready(function()
{
	$('#customer_form').validate({
		submitHandler:function(form)
		{
			$(form).ajaxSubmit({
			success:function(response)
			{
				tb_remove();
				post_person_form_submit(response);
			},
			dataType:'json'
		});

		},
		errorLabelContainer: "#error_message_box",
 		wrapper: "li",
		rules:
		{
			first_name: "required",
			last_name: "required",
    	       		email: "email"
   		},
		messages:
		{
     		first_name: "<?php echo $this->lang->line('common_first_name_required'); ?>",
     		last_name: "<?php echo $this->lang->line('common_last_name_required'); ?>",
     		email: "<?php echo $this->lang->line('common_email_invalid_format'); ?>"
		}
	});
});
</script>
