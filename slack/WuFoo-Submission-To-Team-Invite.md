# Send Team Invite After Form Submission

For this example we are going to use WuFoo to trigger a team invite based on the form data that was submitted.

### Recipe Sample
Depending on how your form is setup you will need to adjust your sample code.

``` javascript
{
  "Field1": "some-email@gmail.com"
}
```

### Recipe

``` javascript
// START: Edit below here.
	// The name of the field/key the email address is in when coming into the system.
	var email_field = "Field1"; 
	// your slack team/hostname
	var slack_hostname = '';
	// If you wish to add an extra message to the invite.
	var extra_message = '';
	// channels to join if different than the account default.
	var auto_join_channels = '';
	// slack auth token - generate at https://api.slack.com
	var slack_auth_token = '';
// END: Edit above here

// Build the invite URL
var invite_url='https://'+slack_hostname+'.slack.com/api/users.admin.invite?t='+Date.now();

var payload = {};

payload.email = message.getBody()[email_field];
payload.channels = auto_join_channels;
payload.token = slack_auth_token;
payload.set_active = true;
payload._attempts = 1;
if(extra_message.length){
	payload.extra_message = extra_message;
}

// Set the details back into the message to be sent...
message.setUrl(invite_url);
message.setBody(payload);
message.setContentType('application/x-www-form-urlencoded');


```
