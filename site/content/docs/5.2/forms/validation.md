---
layout: docs
title: Validation
description: Provide valuable, actionable feedback to your users with HTML5 form validation, via browser default behaviors or custom styles and JavaScript.
group: forms
toc: true
---

## How it works

Here's how form validation works with Bootstrap:

- HTML form validation is applied via CSS's two pseudo-classes, `:invalid` and `:valid`. It applies to `<input>`, `<select>`, and `<textarea>` elements.
- Bootstrap scopes the `:invalid` and `:valid` styles to parent `.was-validated` class, usually applied to the `<form>`. Otherwise, any required field without a value shows up as invalid on page load. This way, you may choose when to activate them (typically after form submission is attempted).
- To reset the appearance of the form (for instance, in the case of dynamic form submissions using Ajax), remove the `.was-validated` class from the `<form>` again after submission.
- As a fallback, `.is-invalid` and `.is-valid` classes may be used instead of the pseudo-classes for [server-side validation](#server-side). They do not require a `.was-validated` parent class.
- Due to constraints in how CSS works, we cannot (at present) apply styles to a `<label>` that comes before a form control in the DOM without the help of custom JavaScript.
- All modern browsers support the [constraint validation API](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#the-constraint-validation-api), a series of JavaScript methods for validating form controls.
- Feedback messages may utilize the [browser defaults](#browser-defaults) (different for each browser, and unstylable via CSS) or our custom feedback styles with additional HTML and CSS.
- You may provide custom validity messages with `setCustomValidity` in JavaScript.

With that in mind, consider the following demos for our custom form validation styles, optional server-side classes, and browser defaults.

## Custom styles

For custom Bootstrap form validation messages, you'll need to add the data-bs-toggle="form" `<form>`. This disables the browser default feedback tooltips, but still provides access to the form validation APIs in JavaScript. Try to submit the form below; our JavaScript will intercept the submit button and relay feedback to you. When attempting to submit, you'll see the `:invalid` and `:valid` styles applied to your form controls.

Custom feedback styles apply custom colors, borders, focus styles, and background icons to better communicate feedback. Background icons for `<select>`s are only available with `.form-select`, and not `.form-control`.

{{< example >}}
<form class="row g-3" data-bs-toggle="form">
  <div class="col-md-4">
    <label for="validationCustom01" class="form-label">First name</label>
    <input type="text" class="form-control" id="validationCustom01" value="Mark" required data-bs-valid="Looks good!" data-bs-invalid="Please, provide a valid Name!">
  </div>
  <div class="col-md-4">
    <label for="validationCustom02" class="form-label">Last name</label>
    <input type="text" class="form-control" id="validationCustom02" value="Otto" required data-bs-valid="Looks good!">
  </div>
  <div class="col-md-4">
    <label for="validationCustomUsername" class="form-label">Username</label>
    <div class="input-group has-validation">
      <span class="input-group-text" id="inputGroupPrepend">@</span>
      <input type="text" class="form-control" id="validationCustomUsername" aria-describedby="inputGroupPrepend" required data-bs-invalid="Please choose a username.">
    </div>
  </div>
  <div class="col-md-6">
    <label for="validationCustom03" class="form-label">City</label>
    <input type="text" class="form-control" id="validationCustom03" required data-bs-invalid="Please provide a valid city.">
  </div>
  <div class="col-md-3">
    <label for="validationCustom04" class="form-label">State</label>
    <select class="form-select" id="validationCustom04" required data-bs-invalid="Please select a valid state.">
      <option selected disabled value="">Choose...</option>
      <option>...</option>
    </select>
  </div>
  <div class="col-md-3">
    <label for="validationCustom05" class="form-label">Zip</label>
    <input type="text" class="form-control" id="validationCustom05" required data-bs-invalid="Please provide a valid zip.">
  </div>
  <div class="col-12">
    <div class="form-check">
      <input class="form-check-input" type="checkbox" value="" id="invalidCheck" required data-bs-invalid="You must agree before submitting.">
      <label class="form-check-label" for="invalidCheck">
        Agree to terms and conditions
      </label>
    </div>
  </div>
  <div class="col-12">
    <button class="btn btn-primary" type="submit">Submit form</button>
    <button class="btn btn-danger" type="reset">Reset form</button>
  </div>
</form>
{{< /example >}}

{{< example lang="js" show_preview="false" >}}
{{< js.inline >}}
{{< /js.inline >}}
{{< /example >}}

## Browser defaults

Not interested in custom validation feedback messages or writing JavaScript to change form behaviors? All good, you can use the browser defaults. Try submitting the form below. Depending on your browser and OS, you'll see a slightly different style of feedback.

While these feedback styles cannot be styled with CSS, you can still customize the feedback text through JavaScript.

{{< example >}}
<form class="row g-3">
  <div class="col-md-4">
    <label for="validationDefault01" class="form-label">First name</label>
    <input type="text" class="form-control" id="validationDefault01" value="Mark" required>
  </div>
  <div class="col-md-4">
    <label for="validationDefault02" class="form-label">Last name</label>
    <input type="text" class="form-control" id="validationDefault02" value="Otto" required>
  </div>
  <div class="col-md-4">
    <label for="validationDefaultUsername" class="form-label">Username</label>
    <div class="input-group">
      <span class="input-group-text" id="inputGroupPrepend2">@</span>
      <input type="text" class="form-control" id="validationDefaultUsername"  aria-describedby="inputGroupPrepend2" required>
    </div>
  </div>
  <div class="col-md-6">
    <label for="validationDefault03" class="form-label">City</label>
    <input type="text" class="form-control" id="validationDefault03" required>
  </div>
  <div class="col-md-3">
    <label for="validationDefault04" class="form-label">State</label>
    <select class="form-select" id="validationDefault04" required>
      <option selected disabled value="">Choose...</option>
      <option>...</option>
    </select>
  </div>
  <div class="col-md-3">
    <label for="validationDefault05" class="form-label">Zip</label>
    <input type="text" class="form-control" id="validationDefault05" required>
  </div>
  <div class="col-12">
    <div class="form-check">
      <input class="form-check-input" type="checkbox" value="" id="invalidCheck2" required>
      <label class="form-check-label" for="invalidCheck2">
        Agree to terms and conditions
      </label>
    </div>
  </div>
  <div class="col-12">
    <button class="btn btn-primary" type="submit">Submit form</button>
  </div>
</form>
{{< /example >}}

## Server-side

We recommend using client-side validation, but in case you require server-side validation, you can indicate invalid and valid form fields with `.is-invalid` and `.is-valid`. Note that `.invalid-feedback` is also supported with these classes.

Ensure that the feedback/error message is associated with the relevant form field using `aria-describedby` (noting that this attribute allows more than one `id` to be referenced, in case the field already points to additional form text).

To fix [issues with border radius](https://github.com/twbs/bootstrap/issues/25110), input groups require an additional `.has-validation` class.

{{< example >}}
<form class="row g-3">
  <div class="col-md-4">
    <label for="validationServer01" class="form-label">First name</label>
    <input type="text" class="form-control is-valid" id="validationServer01" value="Mark" aria-describedby="validationServerNameFeedback" required>
    <div id="validationServerNameFeedback" class="valid-feedback">
      Looks good!
    </div>
  </div>
  <div class="col-md-4">
    <label for="validationServer02" class="form-label">Last name</label>
    <input type="text" class="form-control is-valid" id="validationServer02" aria-describedby="validationServerLastNameFeedback" value="Otto" required>
    <div id="validationServerLastNameFeedback" class="valid-feedback">
      Looks good!
    </div>
  </div>
  <div class="col-md-4">
    <label for="validationServerUsername" class="form-label">Username</label>
    <div class="input-group has-validation">
      <span class="input-group-text" id="inputGroupPrepend3">@</span>
      <input type="text" class="form-control is-invalid" id="validationServerUsername" aria-describedby="inputGroupPrepend3 validationServerUsernameFeedback" required>
      <div id="validationServerUsernameFeedback" class="invalid-feedback">
        Please choose a username.
      </div>
    </div>
  </div>
  <div class="col-md-6">
    <label for="validationServer03" class="form-label">City</label>
    <input type="text" class="form-control is-invalid" id="validationServer03" aria-describedby="validationServer03Feedback" required>
    <div id="validationServer03Feedback" class="invalid-feedback">
      Please provide a valid city.
    </div>
  </div>
  <div class="col-md-3">
    <label for="validationServer04" class="form-label">State</label>
    <select class="form-select is-invalid" id="validationServer04" aria-describedby="validationServer04Feedback" required>
      <option selected disabled value="">Choose...</option>
      <option>...</option>
    </select>
    <div id="validationServer04Feedback" class="invalid-feedback">
      Please select a valid state.
    </div>
  </div>
  <div class="col-md-3">
    <label for="validationServer05" class="form-label">Zip</label>
    <input type="text" class="form-control is-invalid" id="validationServer05" aria-describedby="validationServer05Feedback" required>
    <div id="validationServer05Feedback" class="invalid-feedback">
      Please provide a valid zip.
    </div>
  </div>
  <div class="col-12">
    <div class="form-check">
      <input class="form-check-input is-invalid" type="checkbox" value="" id="invalidCheck3" aria-describedby="invalidCheck3Feedback" required>
      <label class="form-check-label" for="invalidCheck3">
        Agree to terms and conditions
      </label>
      <div id="invalidCheck3Feedback" class="invalid-feedback">
        You must agree before submitting.
      </div>
    </div>
  </div>
  <div class="col-12">
    <button class="btn btn-primary" type="submit">Submit form</button>
  </div>
</form>
{{< /example >}}

## Supported elements

Validation styles are available for the following form controls and components:

- `<input>`s and `<textarea>`s with `.form-control` (including up to one `.form-control` in input groups)
- `<select>`s with `.form-select`
- `.form-check`s

{{< example >}}
<form class="was-validated">
  <div class="mb-3">
    <label for="validationTextarea" class="form-label">Textarea</label>
    <textarea class="form-control" id="validationTextarea" placeholder="Required example textarea" aria-describedby="validationSupportedElementsTextArea" required></textarea>
    <div id="validationSupportedElementsTextArea" class="invalid-feedback">
      Please enter a message in the textarea.
    </div>
  </div>

  <div class="form-check mb-3">
    <input type="checkbox" class="form-check-input" id="validationFormCheck1" aria-describedby="validationSupportedElementsCheckBox" required>
    <label class="form-check-label" for="validationFormCheck1">Check this checkbox</label>
    <div id="validationSupportedElementsCheckBox" class="invalid-feedback">Example invalid feedback text</div>
  </div>

  <div class="form-check">
    <input type="radio" class="form-check-input" id="validationFormCheck2" name="radio-stacked" aria-describedby="validationSupportedElementsRadio" required>
    <label class="form-check-label" for="validationFormCheck2">Toggle this radio</label>
  </div>
  <div class="form-check mb-3">
    <input type="radio" class="form-check-input" id="validationFormCheck3" name="radio-stacked" aria-describedby="validationSupportedElementsRadio" required>
    <label class="form-check-label" for="validationFormCheck3">Or toggle this other radio</label>
    <div id="validationSupportedElementsRadio" class="invalid-feedback">More example invalid feedback text</div>
  </div>

  <div class="mb-3">
    <select class="form-select" required aria-label="select example" aria-describedby="validationSupportedElementsSelect">
      <option value="">Open this select menu</option>
      <option value="1">One</option>
      <option value="2">Two</option>
      <option value="3">Three</option>
    </select>
    <div id="validationSupportedElementsSelect" class="invalid-feedback">Example invalid select feedback</div>
  </div>

  <div class="mb-3">
    <input type="file" class="form-control" aria-label="file example" required aria-describedby="validationSupportedElementsFile">
    <div id="validationSupportedElementsFile" class="invalid-feedback">Example invalid form file feedback</div>
  </div>

  <div class="mb-3">
    <button class="btn btn-primary" type="submit" disabled>Submit form</button>
  </div>
</form>
{{< /example >}}

## Tooltips

If your form layout allows it, you can swap the `.{valid|invalid}-feedback` classes for `.{valid|invalid}-tooltip` classes to display validation feedback in a styled tooltip. Be sure to have a parent with `position: relative` on it for tooltip positioning. In the example below, our column classes have this already, but your project may require an alternative setup.

{{< example >}}
<form class="row g-3" data-bs-toggle="form" data-bs-type="tooltip" >
  <div class="col-md-4 position-relative">
    <label for="validationTooltip01" class="form-label">First name</label>
    <input type="text" class="form-control" id="validationTooltip01" value="Mark" required data-bs-valid="Looks good!">
  </div>
  <div class="col-md-4 position-relative">
    <label for="validationTooltip02" class="form-label">Last name</label>
    <input type="text" class="form-control" id="validationTooltip02" value="Otto" required  data-bs-valid="Looks good!">
  </div>
  <div class="col-md-4 position-relative">
    <label for="validationTooltipUsername" class="form-label">Username</label>
    <div class="input-group has-validation">
      <span class="input-group-text" id="validationTooltipUsernamePrepend">@</span>
      <input type="text" class="form-control" id="validationTooltipUsername" aria-describedby="validationTooltipUsernamePrepend" required data-bs-invalid="Please choose a username.">
    </div>
  </div>
  <div class="col-md-6 position-relative">
    <label for="validationTooltip03" class="form-label">City</label>
    <input type="text" class="form-control" id="validationTooltip03" required data-bs-invalid="Please provide a valid city.">
  </div>
  <div class="col-md-3 position-relative">
    <label for="validationTooltip04" class="form-label">State</label>
    <select class="form-select" id="validationTooltip04" required data-bs-invalid="Please select a valid state.">
      <option selected disabled value="">Choose...</option>
      <option>...</option>
    </select>
  </div>
  <div class="col-md-3 position-relative">
    <label for="validationTooltip05" class="form-label">Zip</label>
    <input type="text" class="form-control" id="validationTooltip05" required data-bs-invalid="Please provide a valid zip.">
  </div>
  <div class="col-12">
    <button class="btn btn-primary" type="submit">Submit form</button>
    <button class="btn btn-danger" type="reset">Reset form</button>
  </div>
</form>
{{< /example >}}

## Sass

### Variables

{{< scss-docs name="form-feedback-variables" file="scss/_variables.scss" >}}

### Mixins

Two mixins are combined together, through our [loop](#loop), to generate our form validation feedback styles.

{{< scss-docs name="form-validation-mixins" file="scss/mixins/_forms.scss" >}}

### Map

This is the validation Sass map from `_variables.scss`. Override or extend this to generate different or additional states.

{{< scss-docs name="form-validation-states" file="scss/_variables.scss" >}}

Maps of `$form-validation-states` can contain three optional parameters to override tooltips and focus styles.

### Loop

Used to iterate over `$form-validation-states` map values to generate our validation styles. Any modifications to the above Sass map will be reflected in your compiled CSS via this loop.

{{< scss-docs name="form-validation-states-loop" file="scss/forms/_validation.scss" >}}

### Customizing

Validation states can be customized via Sass with the `$form-validation-states` map. Located in our `_variables.scss` file, this Sass map is how we generate the default `valid`/`invalid` validation states. Included is a nested map for customizing each state's color, icon, tooltip color, and focus shadow. While no other states are supported by browsers, those using custom styles can easily add more complex form feedback.


## Usage
### Via data attributes

To easily add form validation behavior to you form, add `data-bs-toggle="form"` attribute to the `<form>` element.

### Via JavaScript

Enable manually with:

```js
const formElementList = document.querySelectorAll('form')
const formList = [...formElementList].map(formEl => new bootstrap.Form(formEl))
```

### Options

#### Form
{{< bs-table "table" >}}
| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `type` | string | `feedback` | You may pick the kind of feedback. Acceptable values `tooltip` or `feedback` |
| `validateCallback` | function, null | `null` | A callback to execute while trying to check for errors. Can be use for ajax submissions/validations. |
{{< /bs-table >}}


#### Field
{{< bs-table "table" >}}
| Name | Type | Default | Description |
| --- | --- | --- | --- |
| `invalid` | string | `''` | invalid message to append |
| `valid` | string | `''` | valid message to append |
{{< /bs-table >}}

### Methods


You can create a form instance using the constructor, for example:

```js
const bsForm = new bootstrap.Form('#myForm', { type: 'tooltip' })
```

#### Form
{{< bs-table "table" >}}
| Method | Description |
| --- | --- |
| `getInstance` | *Static* method which allows you to get the form instance associated with a DOM element. |
| `getOrCreateInstance` | *Static* method which allows you to get the form instance associated with a DOM element, or create a new one in case it wasn't initialized. |
| `getElement` | Returns the DOM element of the instance. |
| `getFields` | Returns all form-fields instances of the form. Array\<FormField\>. |
| `getField('name')` | Searches and return the requested FormField instance or undefined. |
| `clear` | Clears all the form validation results. |
| `validate` | Activates validation process.  |
{{< /bs-table >}}

#### Field
{{< bs-table "table" >}}
| Method | Description |
| --- | --- |
| `getInstance` | *Static* method which allows you to get the form Field instance associated with a DOM element |
| `getOrCreateInstance` | *Static* method which allows you to get the form Field instance associated with a DOM element, or create a new one in case it wasn't initialized |
| `getElement` | Returns the DOM element of the instance. |
| `clearAppended` | Clears any appended messages from field. |
| `appendError(message)` | Appends the given message as an error feedback. In case we do not provide a message, it fallbacks to the configuration given `invalid` message. |
| `appendSuccess(message)` | Appends the given message as a success feedback. In case we do not provide a message, it fallbacks to the configuration given `valid` message. |
| `appendFeedback(message)` | Appends the given message as a simple info feedback. |
| `name` | returns the name (fallback to id) of the field as unique identifier between form elements. |
{{< /bs-table >}}