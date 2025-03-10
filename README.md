# jQuery Form Validator 

*Validation framework that let's you configure, rather than code, your validation logic.*

I started writing this plugin back in 2009 and it has given me much joy over the years. But all good things must come to an end and now it's time for this plugin to pull in its oars and go down with history.

**This plugin is no longer being developed!** It supports jQuery v. 1.8 >= 2.2.4. No pull requests will become merged in but feel free to fork and do whatever you like!

[![Travis](https://travis-ci.org/victorjonsson/jQuery-Form-Validator.svg)](https://travis-ci.org/victorjonsson/jQuery-Form-Validator/builds/)

[![npm version](https://badge.fury.io/js/jquery-form-validator.svg)](https://www.npmjs.com/package/jquery-form-validator)

*Usage example*

```html
<form action="" method="POST">
  <p>
    Name (4 characters minimum):
    <input name="user" data-validation="length" data-validation-length="min4" />
  </p>
  <p>
    Birthdate (yyyy-mm-dd):
    <input name="birth" data-validation="birthdate" />
  </p>
  <p>
    Website:
    <input name="website" data-validation="url" />
  </p>
  <p>
    <input type="submit" />
  </p>
</form>
<script src="js/jquery.min.js"></script>
<script src="js/form-validator/jquery.form-validator.min.js"></script>
<script>
    $.validate({
        modules : 'date, security'
    });
</script>
```

### Support for HTML5

This plugin can serve as a fallback solution for the validation attributes in the HTML5 spec. With the html5 module you can use the following native features:

**Attributes**: require, pattern, maxlength, min, max, placeholder

**Input types**: url, date, time, email, number

**Elements**: Use the element `datalist` to create input suggestions


### Default validators and features (no module needed)
 * **url**
 * **email**
 * **domain** — *domain.com*
 * **number** — *float/negative/positive/range/step*
 * **date** — *yyyy-mm-dd (format can be customized, more information below)*
 * **alphanumeric** — *with support for defining additional characters*
 * **length** — *min/max/range*
 * **required** — *no validation except that a value has to be given*
 * **custom** — *Validate value against regexp*
 * **checkboxgroup** — *ensure at least 1 checkbox in group has been selected*
 * Show help information automatically when input is focused
 * Validate given values immediately when input looses focus.
 * Make validation optional by adding attribute data-validation-optional="true" to the element. This means
 that the validation defined in data-validation only will take place in case a value is given.
 * Make validation dependent on another input of type checkbox being checked by adding attribute
 data-validation-if-checked="name of checkbox input"
 * Create input suggestions with ease, no jquery-ui needed
 * to apply multiple validators to an input element, separate the validator names using a space (ex: required email)

Read the documentation for the default features at [#default-validators](#default-validators)

### Module: security
 * **spamcheck**
 * **confirmation**
 * **creditcard**
 * **CVV**
 * **strength** — *Validate the strength of a password*
 * **server** — *Validate value of input on server side*
 * **letternumeric** — *Validate that the input value consists out of only letters and/or numbers*
 * **recaptcha** - *Validate Google [reCaptcha 2](https://www.google.com/recaptcha/intro/index.html)*

Read the documentation for the security module at [#security-validators](#security-validators)

### Module: date
 * **time** — *hh:mm*
 * **birthdate** — *yyyy-mm-dd, not allowing dates in the future or dates that's older than 122 years (format can be customized, more information below)*

Read the documentation for the date module at [#date-validators](#date-validators)

### Module: location
 * **country**
 * **federatestate**
 * **longlat**
 * Suggest countries (english only)
 * Suggest states in the US

Read the documentation for the location module at [#location-validators](/#location-validators)

### Module: file
 * **mime**
 * **extension**
 * **size** (file size)
 * **dimension** (size dimension and ratio)

Read the documentation for the file module at [#file-validators](#file-validators)

### Module: logic

* **Dependent validation**
* **Require "one-of"**

Read the documentation for this module at [/#logic](#logic)

### Module: sepa

* **IBAN**
* **BIC**
* **Sepa**

Read the documentation for this module at [http://formvalidator.net/#sepa](http://www.formvalidator.net/#sepa)


### Module: sweden
 * **swemob** — *validate that the value is a swedish mobile telephone number*
 * **swesec** — *validate swedish social security number*
 * **county** - *validate that the value is an existing county in Sweden*
 * **municipality** - *validate that the value is an existing municipality in Sweden*
 * Suggest county
 * Suggest municipality

Read the documentation for the Swedish module at [http://formvalidator.net/#sweden-validators](http://www.formvalidator.net/#country-specific-validators_sweden)

### Module: uk
 * **ukvatnumber**
 * **uknin**
 * **ukutr**

Read the documentation for the UK module at [http://formvalidator.net/#uk-validators](http://www.formvalidator.net/#country-specific-validators_uk)

### Module: brazil
 * **brphone** — *Validate a brazilian telephone number*
 * **cep**
 * **cpf**

### Module: poland
 * **plpesel** - *validate polish personal identity number (in Polish identity cards)*
 * **plnip** - *validate polish VAT identification number*
 * **plregon** - *validate polish bussiness identity number*

### Module: color
 * **hex** - *validate hex color format*
 * **rgb** - *validate rgb color format*
 * **rgba** - *validate rgba color format*
 * **hsl** - *validate hsl color format*
 * **hsla** - *validate hsla color format*

### Module: sanitation
 * **trim**
 * **trimLeft**
 * **trimRight**
 * **upper**  — Convert all letters to upper case
 * **lower**  — Convert all letters to lower case
 * **capitalize**  — Convert the first letter in all words to upper case
 * **insertRight**  — Declare a text that should be inserted at the end of the value, attribute data-sanitize-insert-right
 * **insertLeft**  — Declare a text that should be inserted at the beginning of the value, attribute data-sanitize-insert-left
 * **escape**  — Convert < > & ' " to html entities
 * **strip**  — Comma separated list with words that gets automatically removed
 * **numberFormat**  — Declare the attribute data-sanitize-number-format with any of the formats described on http://numeraljs.com/. Note that this rule requires that numeral.js is included in the page

Read the documentation for the sanitation module at [http://formvalidator.net/#data-sanitation](http://formvalidator.net/#data-sanitation)


## Writing a custom validator
You can use the function `$.formUtils.addValidator()` to add your own validation function. Here's an example of a validator
that checks if the input contains an even number.

```html
<form action="" method="POST">
    <p>
        <input type="text" data-validation="even" />
    </p>
    ...
</form>
<script src="js/jquery.min.js"></script>
<script src="js/form-validator/jquery.form-validator.min.js"></script>
<script>

    // Add validator
    $.formUtils.addValidator({
        name : 'even',
        validatorFunction : function(value, $el, config, language, $form) {
            return parseInt(value, 10) % 2 === 0;
        },
        errorMessage : 'You have to answer an even number',
        errorMessageKey: 'badEvenNumber'
    });

    // Initiate form validation
    $.validate();

</script>
```

### Required properties passed into $.formUtils.addValidator

*name* - The name of the validator, which is used in the validation attribute of the input element.

*validatorFunction* - Callback function that validates the input. Should return a boolean telling if the value is considered valid or not.

*errorMessageKey* - Name of language property that is used in case the value of the input is invalid.

*errorMessage* - An alternative error message that is used if errorMessageKey is left with an empty value or isn't defined
in the language object. Note that you also can use [inline error messages](http://formvalidator.net/#localization) in your form.


The validation function takes these five arguments:
- value — the value of the input thats being validated
- $el — jQuery object referring to the input element being validated
- config — Object containing the configuration of this form validation
- language — Object with error dialogs
- $form — jQuery object referring to the form element being validated

## Creating a custom module

A "module" is basically a javascript file containing one or more calls to [$.formUtils.addValidator()](#writing-a-custom-validator).
The module file must be placed in the same directory as `jquery.form-validator.min.js` if you want it to load automatically via the setup function.

You can use the method `$.formUtils.loadModules` if you want to load the module from a custom path.

```js
$.formUtils.loadModules('customModule otherCustomModule', 'js/validation-modules/');
$.validate({
   modules: 'security, date'
});
```

The first argument of `$.formUtils.loadModules` is a comma separated string with names of module files, without
file extension.

The second argument is the path where the module files are located. This argument is optional, if not given
the module files has to be located in the same directory as the core modules shipped together with this jquery plugin
(js/form-validator/)

## Show help information
It is possible to display help information for each input. The information will fade in when input is focused and fade out when input looses focus.

```html
<form action="" id="my_form">
	<p>
	  <strong>Why not:</strong>
	  <textarea name="why" data-validation-help="Please give us some more information" data-validation="required"></textarea>
	</p>
	...
```

## Fully customizable

Read about how to customize this plugin over at [http://formvalidator.net/#configuration](http://formvalidator.net/#configuration)

### Validate On Event ###
You can cause an element to be validated upon the firing of an event, by attaching an attribute to the form input element named `data-validation-event="click"`. When the configuration settings have `validateOnEvent : true`, the click event will trigger the onBlur validaton for that element. Possible use case: Checkboxes. Instead of waiting for the checkbox to lose focus (blur) and waiting for a validation to occurr, you can specify that elements validation should occur as soon as that checkbox element is clicked.

## Localization

This plugin comes with translations for English, Polish,
  Romanian,
  Danish,
  Norwegian,
  Dutch,
  Czech,
  Catalan,
  Russian,
  Italian,
  French,
  German,
  Swedish and
  Portuguese. You can also choose to override the error
dialogs yourself. Here you can read more about [localization](http://formvalidator.net/#localization)

# Default validators

### Answer length (required)

```
<!-- Require an answer (can be applied to all types of inputs and select elements) -->
<input type="text" data-validation="required">
<input type="checkbox" name="agreement" data-validation="required">
<select name="answer" data-validation="required">
  <option value=""> - - Answer - - </option>
  <option>Yes</option>
  <option>No</option>
</select>

<!-- Max 100 characters -->
<input type="text" data-validation="length" data-validation-length="max100">

<!-- Minimum 20 characters -->
<input type="text" data-validation="length" data-validation-length="min20">

<!-- No less than 50 characters and no more than 200 characters -->
<input type="text" data-validation="length" data-validation-length="50-200">

<!-- Require that atleast 2 options gets choosen -->
<select multiple="multiple" size="5" data-validation="length" data-validation-length="min2">
  <option>A</option>
  <option>B</option>
  <option>C</option>
  <option>D</option>
  <option>E</option>
</select>
```
This plugin also supports the attributes "required" and "maxlength" by using the Html5 module.

### Numbers
```
<!-- Any numerical value -->
<input type="text" data-validation="number">

<!-- Only allowing float values -->
<input type="text" data-validation="number" data-validation-allowing="float">

<!-- Allowing float values and negative values -->
<input type="text" data-validation="number" data-validation-allowing="float,negative">

<!-- Validate float number with comma separated decimals -->
<input type="text" data-validation="number" data-validation-allowing="float" 
		 data-validation-decimal-separator=",">

<!-- Only allowing numbers from 1 to 100 -->
<input type="text" data-validation="number" data-validation-allowing="range[1;100]">

<!-- Only allowing numbers from -50 to 30 -->
<input type="text" data-validation="number" data-validation-allowing="range[-50;30],negative">

<!-- Only allowing numbers from 0.05 to 0.5 -->
<input type="text" data-validation="number" data-validation-allowing="range[0.05;0.5],float">
You can also define the decimal separator when initializing the validation.

<p>
    <strong>Average points</strong><br>
    <input type="text" data-validation="number" data-validation-allowing="float">
  </p>
  ....
</form>
<script>
  $.validate({
    decimalSeparator : ','
  });
</script>
```
Inputs of type "number" will also become validated by loading the html5 module.

### E-mail
```
<input type="text" data-validation="email">
```
Inputs of type "email" will also become validated by loading the html5 module.

### URL:s

```
<input type="text" data-validation="url">
```
Inputs of type "url" will also become validated by loading the html5 module.

### Date

```
<!-- Validate date formatted yyyy-mm-dd -->
<input type="text" data-validation="date">

<!-- Validate date formatted yyyy-mm-dd but dont require leading zeros -->
<input type="text" data-validation="date" data-validation-require-leading-zero="false">

<!-- Validate date formatted dd/mm/yyyy -->
<input type="text" data-validation="date" data-validation-format="dd/mm/yyyy">
```

See the date module for further validators.

### Alphanumeric

```
<!-- This input requires an answer that contains only letters a-z and/or numbers -->
<input type="text" data-validation="alphanumeric">

<!-- This input requires the same as the one above but it also allows hyphen and underscore -->
<input type="text" data-validation="alphanumeric" data-validation-allowing="-_">
```
If you want to allow any kind of letters (not only A-Z) you're looking for the letternumeric validator.

### Checkboxes Group
Validate qty of checkboxes in a group (same name) have been checked, using min, max or range. Only the first checkbox element in the group needs to have the validation attributes added.
```
<!-- Require checkboxes in this group, min1 -->
<input type="checkbox" name="newsletters[]" data-validation="checkbox_group" data-validation-qty="min1">
<!-- Require checkboxes in this group, max3 -->
<input type="checkbox" name="newsletters[]" data-validation="checkbox_group" data-validation-qty="max3">
<!-- Require checkboxes in this group, min1, max4 -->
<input type="checkbox" name="newsletters[]" data-validation="checkbox_group" data-validation-qty="1-4">
If your checkboxes group is generated by a server-side script and you don't want to add the validation attributes to each input element, you can use this javascript snippet before calling the validatorLoad() function

<!-- Add validation attributes to first input element in
 checkboxes group, before loading validator -->
<script>
$("[name='newsletters[]']:eq(0)")
  .valAttr('','validate_checkbox_group')
  .valAttr('qty','1-2')
  .valAttr('error-msg','chose 1, max 2');
</script>
Regexp
<!-- This input would only allow lowercase letters a-z -->
<input type="text" data-validation="custom" data-validation-regexp="^([a-z]+)$">
```

This plugin also supports the attribute "pattern" by using the Html5 module.

### Character count down
```
<p>
    History (<span id="maxlength">50</span> characters left)
    <textarea rows="3" id="area"></textarea>
  </p>
<script>
  $('#area').restrictLength($('#maxlength'));
</script>
```
### Make validation optional
```
<!-- This input will only be validated if a value is given -->
<input type="text" data-validation="url" data-validation-optional="true">
```
You can also use the logic module if you want the validation of an input depend on another input having a value.

### Display help text
It is possible to display help information beside each input. The text will fade in when the input gets focus on and fade out when the input looses focus. The container for the help text will have the class form-help. If you don't want this feature you can read the setup guide on how to disable it.

```
<form action="" id="some-form">
    <p>
      <strong>Why not?</strong>
      <input name="why" data-validation-help="Please give us some more information">
    </p>
    ...
  </form>
  ```
### Validate inputs when blurred

By default each input will become validated immediately when the input looses focus. If you don't want this feature you can read the setup guide on how to disable it.

### Input suggestions
There are two ways you can give suggestions to the user while the user types.

1) Using attribute data-suggestions

```
<p>
    What's your favorite color?
    <input name="color" data-suggestions="White, Green, Blue, Black, Brown">
  </p>
  ...
</form>
```
2) Using $.formUtils.suggest()
```
<script>
  var largeArray = [];
  largeArray.push('Something');
  largeArray.push('Something else');
  ...

  $.formUtils.suggest( $('#the-input'), largeArray );
</script>
```
This plugin also supports the data-list element by using the Html5 module.

Ignoring characters
You can tell any validator to ignore certain characters by using the attribute data-validation-ignore (comma separated list).
```
<p>
  How much do you want to donate?
  <!-- Make it optional to end the amount with a dollar-sign -->
  <input name="color" data-validation="number" data-validation-ignore="$">
</p>
```

## Security validators<

### Password confirmation

This validator can be used to validate that the values of two inputs are the same. The first input should have a name suffixed with <em>_confirmation</em> and the second should have the same name but without the suffix.

```
<p>
    Password (at least 8 characters)
    <input name="pass_confirmation" data-validation="length" data-validation-length="min8">

    Confirm password
    <input name="pass" data-validation="confirmation">
</p>
```

```
<p>
    E-mail
    <input name="user-email" data-validation="email" />

    Repeat e-mail
    <input name="repeat" data-validation="confirmation" data-validation-confirm="user-email" />
</p>
```

### Password strength

Use this validator to make sure that your user has a strong enough password. Set attribute <code>data-validation-strength</code> to 1, 2 or 3 depending on how strong password you require.

If you want the strength of the password to be displayed while the user types you call <code>displayPasswordStrength()</code> in the end of the form.

```
<form action="">
    <p>
        <strong>Password:</strong>
        <input name="pass" type="password" break=""
                data-validation="strength" break="" data-validation-strength="2">
    </p>
    ...
</form>

<script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/jquery-form-validator/2.3.26/jquery.form-validator.min.js"></script>
<script>
$.validate({
    modules : 'security',
    onModulesLoaded : function() {
        var optionalConfig = {
            fontSize: '12pt',
            padding: '4px',
            bad : 'Very bad',
            weak : 'Weak',
            good : 'Good',
            strong : 'Strong'
        };

        $('input[name="pass"]').displayPasswordStrength(optionalConfig);
    }
});
</script>
```

### Server side validation

By using this validator you can validate the value given by the user on the server before the form gets submitted. The validation function will send a POST request to the URL declared in <code>data-validation-url</code>. The argument posted to the URL will have the same name as the input being validated.

The form will get the class <em>validating-server-side</em> while the server is being requested.

The response from the validation script must be a JSON formatted object, containing the properties "valid" and "message".

```
{
    "valid" : true|false,
    "message" : "String with text that should be displayed as error message"
}
```

#### Form

```
<form action="">
    <p>
        <strong>User name:</strong>
        <input name="user" data-validation="server" data-validation-url="/validate-input.php">
    </p>
    ...
</form>
```

#### /validate-input.php

```
<?php
$response = array(
    'valid' => false,
    'message' => 'Post argument "user" is missing.'
);

if( isset($_POST['user']) ) {
    $userRepo = new UserRepository( DataStorage::instance() );
    $user = $userRepo->loadUser( $_POST['user'] );

    if( $user ) {
        // User name is registered on another account
        $response = array('valid' => false, 'message' => 'This user name is already registered.');
    } else {
        // User name is available
        $response = array('valid' => true);
    }
}
echo json_encode($response);
```

**Modifying the server request**

The parameter containing the input value, sent to the server, will by default have the same name as the input. You can however set your own parameter name by using the attribute <code>data-validation-param-name</code>. You can also send along other parameters to the server by using the attribute <code>data-validation-req-params</code>.

```
<?php
  $json = json_encode(array('user'=>$user->get('ID')));
?>
<p>
  <strong>E-mail:</strong>
  <input type="email" name="check-email" data-validation="server"
              data-validation-url="/validate-form-input.php"
              data-validation-param-name="email"
              data-validation-req-params="<?php echo $json ?>" />
</p>
```

### Credit card validation

This validator makes it possible to validate any of the credit cards VISA, Mastercard, Diners club, Maestro, CJB, Discover and American express

```
<-- Accept credit card number from Visa, Mastercard and American Express -->
<p>
    Credit card number
    <input data-validation="creditcard" data-validation-allowing="visa, mastercard, amex" />
</p>
<p>
    Security code (cvv)
    <input name="cvv" data-validation="cvv" />
</p>
```

You can also let the user choose a credit card and programmatically change the allowed credit card on the input of the card number.

```
<p>
    Credit card
    <select name="credit-card" id="credit-card">
        <option value="visa">VISA</option>
        <option value="mastercard">Mastercard</option>
        <option value="amex">American express</option>
        <option value="diners_club">Diners club</option>
        <option value="discover">Discover</option>
        <option value="cjb">CJB</option>
        <option value="maestro">Maestro</option>
    </select>
</p>
<p>
    Credit card number
    <input name="creditcard_num" data-validation="creditcard" data-validation-allowing="visa" />
</p>
...
</div>
<script>
$.validate({
    modules : 'security',
    onModulesLoaded : function() {
        // Bind card type to card number validator
        $('#credit-card').on('change', function() {
            var card = $(this).val();
            $('input[name="creditcard_num"]').attr('data-validation-allowing', card);
        });
    }
});
</script>
```

### Simple captcha

```
<?php
session_start();
if( isset($_POST['captcha']) && isset($_SESSION['captcha'])) {
    if( $_POST['captcha'] != ($_SESSION['captcha'][0]+$_SESSION['captcha'][1]) ) {
        die('Invalid captcha answer');  // client does not have javascript enabled
    }
    // process form data
    ...
}
$_SESSION['captcha'] = array( mt_rand(0,9), mt_rand(1, 9) );
?>
<form action="">
    <p>
        What is the sum of <?=$_SESSION['captcha'][0]?> + <?=$_SESSION['captcha'][1]?>?
        (security question)
        <input name="captcha" data-validation="spamcheck"
                    data-validation-captcha="<?=( $_SESSION['capthca'][0] + $_SESSION['captcha'][1] )?>"/>
    </p>
    <p><input type="submit" /></p>
</form>
```

### Google reCAPTCHA

Use this validator if wanting to integrate the Google service reCAPTCHA.

``` 
<p>
    <input  data-validation="recaptcha" data-validation-recaptcha-sitekey="[RECAPTCHA_SITEKEY]">
</p>
```

You can also use the setup function to configure the recaptcha service.

```
$.validate({
    reCaptchaSiteKey: '...',
    reCaptchaTheme: 'light'
});
```

### Letters and numbers

By using the validator <code>letternumeric</code> you can validate that given input value only contains letters and/or numbers. This validator allows any type of character in contrast to the <a href="#default-validators_alphanumeric">alphanumeric</a> validator, which only allows letters A-Z.

```
<!-- This input requires an answer that contains only letters and/or numbers -->
<input type="text" data-validation="letternumeric">

<!-- This input requires the same as the one above but it also allows hyphen and underscore -->
<input type="text" data-validation="alphanumeric" data-validation-allowing="-_">
```

## Date validators

### Birthdate

This validator is the same as the default <a href="#default-validators_dates">date validator</a> except that it only allows past dates and dates that is not older than 120 years.

```
<!-- Validate birth date formatted yyyy-mm-dd -->
<input type="text" data-validation="birthdate">

<!-- Validate birthdate formatted yyyy-mm-dd but dont require leading zeros -->
<input type="text" data-validation="birthdate" data-validation-require-leading-zero="false">

<!-- Validate birth date formatted dd/mm/yyyy -->
<input type="text" data-validation="birthdate" data-validation-format="dd/mm/yyyy">
```

## Time

```
<!-- Validate time formatted HH:mm -->
<input type="text" data-validation="time">
```


## Location validators

### Country

```
<!-- Validate country (english only) -->
<input type="text" data-validation="country"/>
```

### State (US)

```
<!-- Validate US state -->
<input type="text" data-validation="federatestate"/>
```

### Longitude and Latitude

```
<!-- Validate longitude and latitude (eg 40.714623,-74.006605) -->
<input type="text" data-validation="longlat"/>
```

### Suggest country/state

By using this function you'll make it easier for your visitor to input a country or state.

```
    <form action="">
        ...
        <p>
            <strong>Which country are you from?</strong>
            <input name="user_country" data-validation="country"/>
        </p>
        <p>
            <strong>Which state do you live in?</strong>
            <input name="user_home_state" data-validation="federatestate"/>
        </p>
    </form>
</div>
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/jquery-form-validator/2.3.26/jquery.form-validator.min.js"></script>
<script>
$.validate({
    modules : 'location',
    onModulesLoaded : function() {
        $('input[name="user_country"]').suggestCountry();
        $('input[name="user_home_state"]').suggestState();
    }
});
</script>
```

## File validators

### File size

This validation is only supported by Internet Explorer 10, Mozilla FireFox v >= 3.6 and any of the later versions of webkit based browsers.

```
<!-- Validate that file isn't larger than 512 kilo bytes -->
<input type="file" data-validation="size" data-validation-max-size="512kb" />

<!-- Validate that file isn't larger than 3 mega bytes -->
<input type="file" data-validation="size" data-validation-max-size="3M" />
```

### File type

This validation will fall back on checking the file extension in older browsers. In modern browsers the validation will check that any of the extensions in <code>data-validation-allowing</code> exists in the mime type declaration of the file. This means that <code>data-validation-allowing="pdf"</code> will work in both modern browsers (checking against "application/pdf") and older browsers (checking the file extension ".pdf").

```
<!-- Validate that file is an image of type JPG, GIF or PNG and not larger than 2 mega bytes -->
<input type="file" data-validation="mime size" break0="" data-validation-allowing="jpg, png, gif" break=""
       data-validation-max-size="2M" />

<!-- Validate that a file is given and that it has .txt as extension -->
<input type="file" data-validation="required extension" data-validation-allowing="txt" />
```

Validating multiple files (with separate error messages depending on failed validation):

```
<input type="file" multiple="multiple" name="images"
    data-validation="length mime size"
    data-validation-length="min2"
    data-validation-allowing="jpg, png, gif"
    data-validation-max-size="512kb"
    data-validation-error-msg-size="You can not upload images larger than 512kb"
    data-validation-error-msg-mime="You can only upload images"
    data-validation-error-msg-length="You have to upload at least two images"
    />
```

### Image dimension and ratio

Use the validator <code>dimension</code> to check the dimension of an image (jpg, gif or png).

```
<!-- Validate that the image is no smaller than 100x100px -->
<input data-validation="dimension mime" data-validation-allowing="jpg" break="" data-validation-dimension="min100" />

<!-- Validate that the image is no smaller than 300x500 px (width/height) -->
<input data-validation="dimension mime" data-validation-allowing="jpg" break="" data-validation-dimension="min300x500" />

<!-- Validate that the image is no larger than 500x1000 px -->
<input data-validation="dimension mime" data-validation-allowing="jpg" break="" data-validation-dimension="max500x1000" />

<!-- Validate that the image is no smaller than 100x100 px and no larger than 800x800 -->
<input data-validation="dimension mime" data-validation-allowing="jpg" break="" data-validation-dimension="100-800" />

<!-- Validate that the image is no smaller than 200x400 px and no larger than 600x1200 -->
<input data-validation="dimension mime" data-validation-allowing="jpg" break="" data-validation-dimension="200x400-600x1200" />
```

Use the attribute <code>data-validation-ratio</code> to validate that the uploaded image has a certain ratio

```
<!-- Validate that only square images gets uploaded -->
<input data-validation="ratio mime" data-validation-allowing="jpg, png, gif" break="" data-validation-dimension="min100" data-validation-ratio="1:1" />

<!-- Validate that only somewhat square images gets uploaded -->
<input data-validation="ratio mime" data-validation-allowing="jpg" break="" data-validation-dimension="min100" data-validation-ratio="8:10-12:10" />
```

## Logic

### Validators depending on each other

Use the attributes <code>data-validation-depends-on</code> to configure that an input is optional as long as another input is left without an answer.

```
<!-- Require e-mail only if checkbox is checked -->
<p>
    <strong>Contact me:</strong>
    <input name="do-contact" type="checkbox" value="1" />
</p>
<p>
    <strong>E-mail:</strong>
    <input
           type="text"
           data-validation="email"
           data-validation-depends-on="do-contact"
    />
</p>
```

```
<!-- Require a state to be given if the user comes from either USA or Canada -->
<p>
    <strong>Country:</strong>
    <input
           type="text"
           name="country"
           id="country-input"
           data-validation="country"
    />
</p>

<p>
    <strong>State:</strong>
    <input type="text"
           name="state" break=""
           data-validation="required" break1=""
           data-validation-depends-on="country" break2=""
           data-validation-depends-on-value="usa, canada"
    />
</p>
</div>
...
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/jquery-form-validator/2.3.26/jquery.form-validator.min.js"></script>
<script>
$.validate({
    modules : 'location, logic',
    onModulesLoaded : function() {
        $('#country-input').suggestCountry();
    }
});
</script>
```

### Require only one out of several inputs

Use the attribute <code>data-validation-optional-if-answered</code> to tell the validator that only one, out of a group of inputs, requires an answer.

```
<p>
    <strong>Home phone number:</strong>
    <input name="home-phone"
           data-validation="number" break=""
            data-validation-optional-if-answered="cell-phone, work-phone" />
</p>
<p>
    <strong>Cell phone number:</strong>
    <input name="cell-phone"
           data-validation="number" break=""
            data-validation-optional-if-answered="home-phone, work-phone" />
</p>
<p>
    <strong>Work phone number:</strong>
    <input name="work-phone"
           data-validation="number" break=""
            data-validation-optional-if-answered="home-phone, cell-phone" />
</p>
</div>
```

## Changelog

#### 2.3.19
- New translations (Polish, Romanian, Danish, Norwegian, Dutch, Czech, Russian, Italian)
- Several improvements made to already existing translations
- "Validation help" no longer puts constraints on input names
- Improved confirmation validation
- Config parameter `errorMessagePosition` is now only used to point out where error message should be placed. New configuration parameters is introduced that handles custom positioning of error messages [#226](https://github.com/victorjonsson/jQuery-Form-Validator/issues/226#issuecomment-191233456)
- Now possible to add `data-validation-ignore` to filter out certain characters before validation
- New sanitation method `strip` that removes defined characters
- Now possible to declare attributes not prefixed with data-validation in jsconf module
- All inputs gets sanitized on page load when using sanitation module
- Allow dates to omit leading zero using `data-validation-require-leading-zero="false"`
- Module toggleDisabled now acts on value change, not only mouse click
- `data-validation-if-checked` now deprecated, use `data-validation-depends-on` instead [#153](https://github.com/victorjonsson/jQuery-Form-Validator/issues/153)
- Event `beforeValidation` now gets value, language and configuration as arguments and can be used to prevent validation of the input.
- Security module now has a `recaptcha` validator that uses Google reCaptcha 2
- The plugin is installable using npm (also possible to require validation modules when using browserify)
- Polish validation module
- Brazilian validation module
- UK validation module now also have validators `uknin` `ukutr`
- Sepa-module that makes it possible to validate sepa, iban and bic.
- New module named "logic" containing the features `data-validation-depends-on` and `data-validation-optional-if-answered`

#### 2.2.8
- The plugin is now again possible to install via bower.
- Portoguese language pack and validators
- New module used for data-sanitiation
- E-mail addresses now validated in accordance to rfc 6531
- Now possible to use $.fn.validate to programmatically validate inputs
- Hidden inputs won't get validated by default (can be overriden using option validateHiddenInputs)


#### 2.2.43
- Fixed min/max parse error in HTML5 module
- Now also supports Twitter bootstraps horizontal forms
- This plugin now also distributes a default CSS theme including success/fail icons (used on formvalidator.net)
- Email validation now won't fail if email begins with a number
- This plugin now comes with error dialogs translated to English, French, German, Spanish and English.
- New validator `letternumeric`. Validates that input consists out of any type of letter (not only alphanumeric) and/or numbers
- You can now validate image dimension and ratio
- ... and a bunch of other smaller bug fixes and improvements.

#### 2.2.0
* Now possible to define an error message for each validation rule on a certain input (issue #113)
* This plugin now serves as a html5 fallback. You can now use the native attributes to declare which type
of validation that should be applied.
* Use a template for error messages when having errorMessagePosition set to top
* Added validation of credit card number and CVV to the security module
* Event onElementValidate added
* Use the attribute data-validation-confirm to declare which input that should be confirmed when using validation=confirmation (issue #112)
* Validation "required" now supports inputs of type radio
* $.validateForm is now deprecated, use $.isValid instead
* Possible to check if form is valid programmatically without showing error messages
* Select elements can now be validated server-side
* Cleaned up dialog messages
* Various IE8 fixes
* Possible to send along parameters to the server when using server side validation
* Now possible to set your own parameter name when using server side validation
* Improved/simplified URL validation
* ... and a whole lot more small improvements

#### 2.1.47
* Incorrect error-styling when using datepicker or suggestions is now fixed
* Incorrect error-styling of select elements is now fixed
* Deprecated function $.validationSetup is now removed, use $.validate() instead
* You can now return an array with errors using the event `onValidate`
* You can now declare an element where all error messages should be placed (config.errorMessagePosition)

#### 2.1.36
* Now possible to use the native reset() function to clear error messages and error styling of the input elements

#### 2.1.34
* General improvements and bug fixes
* Added events "beforeValidation" and "validation" (see http://formvalidator.net/#configuration_callbacks for more info)

#### 2.1.27
 * E-mail validation support .eu top domain
 * Improvements in server validation
 * Now possible to re-initiate the validation. This makes it possible to dynamically change the form and then call $.validate() again to refresh the validation (issue #59)
 * Number validation now supports range

#### 2.1.15
 * E-mail addresses can now contain + symbol
 * Correction of the US states in validation "federatestate"
 * Fixed bug in server validation

#### 2.1.09
 * File validation now support multiple files
 * Length validation can now be used to validate the number of uploaded files using a file input that supports multiple files
 * Validation classes is no longer applied on inputs that for some reason shouldn't become validated

#### 2.1.08
 * Now possible to configure the decimal separator when validating float values. Use either the
 attribute *data-validation-decimal-separator* or the property *decimalSeparator* when
calling $.validate()
 * $.validationSetup is renamed to $.validate. You will still be able to initiate the validation by calling
 the $.validationSetup but it's considered deprecated.

#### 2.1.06
 * Modules can now be loaded from remote websites

#### 2.1.05
 * Fixed language bug (issue #43 on github)
 * Validation on server side is now triggered by the blur event
 * Now using class names that's compliant with twitter bootstrap 3.x

#### 2.1
 * Code refactoring and some functions renamed
 * Validator "checkbox_group" added

#### 2.0.7
 * Now possible to validate file size, extension and mime type (using the file module)

#### 2.0
 * [min|max]_length is removed (now merged with length validation).
 * The number, int and float validation is merged together, all three variants is now validated by the number validation.
 * Phone validation is moved to "sweden" module and renamed to swephone.
 * The attribute to be used when defining the regular expression for custom validations is now moved to its own attribute (data-validation-regexp)
 * Length validation now looks at attribute data-validation-length (eg. min5, max200, 3-12).
 * The validation rule no longer needs to be prefixed with "validate_" (it's still possible to use the prefix but it's considered deprecated).
 * Some validation functions is moved to modules (see the function reference over at http://formvalidator.net).
 * Added function $.validationSetup() to reduce the amount of code that has to be written when initiating the form validation.


## Credits

http://www.formvalidator.net/#credits
