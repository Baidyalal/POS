<div id="required_fields_message"><?php echo $this->lang->line('common_fields_required_message'); ?></div>
<ul id="error_message_box"></ul>
<?php
	echo form_open('sales/add/',array('id'=>'sale_form'));
?>

<fieldset id="item_basic_info">
<legend><?php echo $this->lang->line("sales_new_item"); ?></legend>

<div class="field_row clearfix">
<?php echo form_label($this->lang->line('items_item_number').':', 'name',array('class'=>'required wide')); ?>
	<div class='form_field'>
	<?php echo form_input(array(
		'name'=>'item_number',
		'id'=>'item_number',
		'value'=>'')
	);?>
	</div>
</div>

<div class="field_row clearfix">
<?php echo form_label($this->lang->line('items_category').':', 'name',array('class'=>'required wide')); ?>         
	<div class='form_field'>
<?php echo form_dropdown('category', array(
		''	=>'-----select-----',
		'Formal'    => 'Formal',
		'Casual'    => 'Casual',
		'Other'   => 'Other'));
	?>
	</div>
</div>

<div class="field_row clearfix">
<?php echo form_label($this->lang->line('items_item_quantity').':', 'name',array('class'=>'required wide')); ?>
	<div class='form_field'>
	<?php echo form_input(array(
		'name'=>'item_quantity',
		'id'=>'item_quantity')
	);?>
	</div>
</div>

<div class="field_row clearfix">
<?php echo form_label($this->lang->line('recvs_discount').':', 'name',array('class'=>'wide')); ?>
	<div class='form_field'>
	<?php echo form_input(array(
		'name'=>'discount',
		'id'=>'discount')
	);?>
	</div>
</div>

<div class="field_row clearfix">
<?php echo form_label($this->lang->line('sales_order_remark').':', 'description',array('class'=>'wide')); ?>
	<div class='form_field'>
	<?php echo form_textarea(array(
		'name'=>'description',
		'id'=>'description',
		'rows'=>'5',
		'cols'=>'17')
	);?>
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
<?php echo form_close();?>
<script type='text/javascript'>

//validation and submit handling
$(document).ready(function()
{
	$("#item_number").autocomplete("<?php echo site_url('items/suggest_item_id');?>",{max:100,minChars:0,delay:10});
 	$("#item_number").result(function(event, data, formatted){});
	$("#item_number").search();

	$('#sale_form').validate({
		submitHandler:function(form)
		{
			/*
			make sure the hidden field #item_number gets set
			to the visible scan_item_number value
			*/
			$('#item_number').val($('#scan_item_number').val());
			$(form).ajaxSubmit({
			success:function(response)
			{
				tb_remove();
				post_item_form_submit(response);
			},
				dataType:'add'
		});
document.forms["sale_form"].submit();
		},
		errorLabelContainer: "#error_message_box",
 		wrapper: "li",
		rules:
		{
			name:"required",
			category:"required",
			item_number:
			{
				required:true,
			},
			category:
			{
				required:true,
			},
			item_quantity:
			{
				required:true,
				number:true
			}
		
   		},
		messages:
		{
			name:"<?php echo $this->lang->line('items_name_required'); ?>",
			category:"<?php echo $this->lang->line('items_category_required'); ?>",
			item_number:
			{
				required:"<?php echo $this->lang->line('items_fabric_code_required'); ?>"
			},
			category:
			{
				required:"<?php echo $this->lang->line('items_style_required'); ?>"
			},
			item_quantity:
			{
				required:"<?php echo $this->lang->line('items_quantity_required'); ?>",
				number:"<?php echo $this->lang->line('items_quantity_number_required'); ?>"
			}

		}
	});
});
</script>
