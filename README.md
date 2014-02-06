# Use it without bootstrap

![Screenshot](screenshot.png "bootstrap.validator.js")

###HTML
	<input
		name="name"
		type="text"

		data-title="This is a message show after validation failed"
		data-regex="^[a-z]{1,10}"
		data-require=""
		data-equals="name_of_the_second_field"
	/>

###Javascript
	$(selector).validate({
		init: function() {

		},
		success: function() {

		},
		fail: function(invalids) {

		}
	})

* data-title: Error description. With $(invalids[i]).attr('data-title') you can get it. For bootstrap3Validate just put it there you don't need to do anything
* data-regex: Validation regex. You can also put 'email' and 'tel'
* data-require: required or not
* data-equals: To check value of 2 field are same or not. Just add it to first one.

# Use it with bootstrap3
###CSS
	form .alert,
	form .process
	{
		display: none;
	}
###HTML
	<form method="POST" action="some_url_to_post_there">
		<fieldset>
			<div class="form-group">
				<label class="control-label">Sample:</label>
				<input name="name" class="form-control" placeholder="Sample item" data-title="Sample message" data-require="" data-regex="^[a-zA-Z]{1,30}$" />
			</div>
			<div class="form-group">
				<label class="control-label">Email:</label>
				<input name="name" class="form-control" placeholder="Your email" data-title="Please use valid email address" data-require="" data-regex="email" />
			</div>
			<div class="form-group">
				<label class="control-label">Select</label>
				<select class="form-control" data-require="" name="select">
					<option value="">Select one item please</option>
					<option value="value1">Item1</option>
					<option value="value2">Item2</option>
				</select>
			</div>
			<div class="form-group">
				<div class="checkbox">
					<label class="control-label">
						<input data-require="" name="accept" type="checkbox" value="true"> Accept?
					</label>
				</div>
			</div>
			<div class="progress progress-striped active">
				<div class="progress-bar"  role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">
					<span class="sr-only">Please wait...</span>
				</div>
			</div>
			<div class="alert alert-danger">

			</div>
			<div class="alert alert-success">
				Sent!
			</div>
			<div class="form-group text-center">
				<button class="btn btn-default" type="submit">Submit</button>
			</div>
		</fieldset>
	</form>
###Javascript (GET/POST submit)
	$(selector).bootstrap3Validate(); // selector can be 'form'


###Javascript (Ajax submit)
	// selector can be 'form'
	$(selector).bootstrap3Validate(function(e) { 
		e.preventDefault();

		var self = $(this);

		$('.process', self).show();
		$("[type='submit']", self).hide();
		$(".alert-danger", self).hide();

		$.ajax({
			url: self.attr('action'),
			data: self.serialize(),
			type: self.attr('method'),
		})
		.done(function() {
			$("[type='text']", self).val(''); // Clear
		})
		.fail(function() {
			$('.alert-danger', self).text('Error!').show();
		})
		.always(function() {
			$('.process', self).hide();
			$("[type='submit']", self).show();
		});
	})