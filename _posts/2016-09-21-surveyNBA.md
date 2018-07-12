
<html lang='en'>
  <head>
    <meta charset='utf-8'>
    <meta content='IE=edge' http-equiv='X-UA-Compatible'>
    <meta content='width=device-width, initial-scale=1' name='viewport'>
  </head>
  <body>
    <!-- Contact Form - sent to a Google Sheet -->
    <form id='foo'>
      <p>
        <label>Name</label>
        <input id='name' name='name' type='text'>
      </p><p>
        <label>Email Address</label>
        <input id='email' name='email' type='email'>
      </p><p>
        <label>Phone Number</label>
        <input id='phone' name='phone' type='tel'>
      </p><p>
        <label>Message</label>
        <textarea id='message' name='message' rows='5'></textarea>
      </p>
        <div id='success'></div>
        <button type='submit'>Send</button>
    </form>

  <script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
  <!-- Custom Theme JavaScript -->
  <script >
// Variable to hold request
var request;

// Bind to the submit event of our form
$("#foo").submit(function(event){

    // Abort any pending request
    if (request) {
        request.abort();
    }
    // setup some local variables
    var $form = $(this);

    // Let's select and cache all the fields
    var $inputs = $form.find("input, select, button, textarea");

    // Serialize the data in the form
    var serializedData = $form.serialize();

    // Let's disable the inputs for the duration of the Ajax request.
    // Note: we disable elements AFTER the form data has been serialized.
    // Disabled form elements will not be serialized.
    $inputs.prop("disabled", true);

    // Fire off the request to /form.php
    request = $.ajax({
        url: "https://script.google.com/macros/s/AKfycbxireXFz8s8Rxv9040N3o0tflxdLdEYx4R-MfePqI6JTMN_KXs/exec",
        type: "post",
        data: serializedData
    });

    // Callback handler that will be called on success
    request.done(function (response, textStatus, jqXHR){
        // Log a message to the console
        console.log("Hooray, it worked!");
        console.log(response);
        console.log(textStatus);
        console.log(jqXHR);
    });

    // Callback handler that will be called on failure
    request.fail(function (jqXHR, textStatus, errorThrown){
        // Log the error to the console
        console.error(
            "The following error occurred: "+
            textStatus, errorThrown
        );
    });

    // Callback handler that will be called regardless
    // if the request failed or succeeded
    request.always(function () {
        // Reenable the inputs
        $inputs.prop("disabled", false);
    });

    // Prevent default posting of form
    event.preventDefault();
});


</script>
</html>