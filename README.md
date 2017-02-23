# form.js
Render a customized lead form at the client-side.

- Supports IE9+.
- Not dependent on jQuery.
- **Vanilla Javascipt.**


###[CodePen Demo](http://codepen.io/fionnachan/pen/jBOPBj)


### 1. Include form.css & form_master.js
### 2. Initialize with or without customized configuration:
```
var x = new fifi_form();
```
OR
```
var form_config = {
  twoStep: false,
  placeholders: {
    first_name: '名字',
    last_name: 'Last Name',
    full_name: 'Full Name',
    birthdate: 'Birth Date',
    email: 'Email',
    phone: 'Phone',
    address: 'Address',
    loc: 'City',
    next: 'Suivre',
    submit: 'Submit'
  },
  locList: { // text: value
    'Choose': '',
    '香港': '香港'
  }
};
var x = new fifi_form(form_config);
```
### Does not recommend having several forms on the same page because there are some minor bugs causing problems. (Will be fixed soon.)

###Full Config:
```
var form_config = {
    formRendered: false, // provide an option to render the form using your own method, but can still use the validation and submission of this form.js
    wrapper: '.form-wrapper', // target element for appending the form
    submissionEndPoint: '/endpoint', // please change to the submission end point of your form
    twoStep: true, // the form can be a one-step form or a two-step form. Submission to the end point happens every time when the "Next" or "Submit" button is clicked
    addressTBC: {
      required: true // if set true, when the "WantsBrochure" checkbox is checked, the user will be required to fill in their address.
    },
    formLogic: {
      WantsBrochure: {
        prechecked: true,
        showOnForm: true,
        labelText: 'I want to order a free brochure.'
      },
      WantsInfo: {
        prechecked: true,
        showOnForm: true,
        labelText: 'I want to receive more information.'
      },
      AcceptTnC: {
        prechecked: true,
        showOnForm: true,
        labelText: 'I accept the <a href="javascript: void(0);" target="_blank">Terms and Conditions</a>.'
      }
    },
    additionalQuestions: [{
      step: 2, // if the form is a one-step form, this number will be ignored.
      isMC: true, // if this is true, answers would be checkboxes.
      radio_or_dropdown: false, // if isMC is true, this is ignored. If isMC is false, the answer should be 'radio' for radio buttons, or 'dropdown' for a select dropdown.
      required: true, // if the form is a two-step form, and the question is on step 2, this will be ignored and be false.
      question: 'How did you hear about us?',
      answers: [
        'from Facebook',
        'from Friends',
        'from Google'
      ]
    }, {
      step: 2,
      isMC: false,
      radio_or_dropdown: 'radio',
      required: false,
      question: 'How long do you want to travel?',
      answers: [
        '2 weeks',
        '4 weeks',
        '3 months'
      ]
    }, {
      step: 2,
      isMC: false,
      radio_or_dropdown: 'dropdown',
      required: true,
      question: 'How long do you want to travel?',
      answers: { // must be "text: value" for dropdown questions
        'Please choose': '',
        '2 weeks': '2w',
        '4 weeks': '4w',
        '3 months': '3m'
      }
    }, {
      step: 1,
      isMC: true,
      radio_or_dropdown: false,
      required: true,
      question: 'Which animals do you like?',
      answers: [
        'Cats',
        'Dogs',
        'Dolphins',
        'Pigs',
        'Ducks',
        'Elephants',
        'Giraffe'
      ]
    }],
    askFullName: true, // if this is true, only full name would be asked, or else there will be a first name field and a last name field.
    showPlaceholder: false, // you can choose to show the placeholder.
    placeholders: { // these placeholders are also used as labels above each input field.
      first_name: 'First Name',
      last_name: 'Last Name',
      full_name: 'Full Name',
      birthdate: 'Birth Date',
      email: 'Email',
      phone: 'Mobile Phone',
      loc: 'City',
      address: 'Address',
      next: 'Next',
      submit: 'Submit'
    },
    autocomplete: {
      use: true, // this cannot be disabled yet. Will fix soon.
      autolist: {
        first_name: {
          name: 'fname',
          auto: 'given-name'
        },
        last_name: {
          name: 'lname',
          auto: 'family-name'
        },
        full_name: {
          name: 'fname',
          auto: 'name'
        },
        email: {
          name: 'email',
          auto: 'email'
        },
        phone: {
          name: 'phone',
          auto: 'tel'
        },
        address: {
          name: 'address',
          auto: 'street-address'
        }
      }
    },
    locList: { // text: value; if this object has only 2 options, the City dropdown will be hidden and not required. It will always be required to choose if it's shown on the form.
      'Choose': '',
      '北京': '11|北京',
      '重庆': '50|重庆'
    },
    customSubmitSuccess: function() {
      document.querySelector('body').style.background = 'white'; // you can customized what to do after successful submissions.
    },
    customSubmitError: function() {
      document.querySelector('body').style.background = '#ffddee'; // you can customized what to do if the user-filled form cannot pass the validation.
    },
    onEachValidationSuccess: function() {
      document.querySelector('body').style.background = 'red'; // you can customized what to do every time a required field passed the validation.
    },
    onEachValidationError: function() {
      document.querySelector('body').style.background = 'blue'; // you can customized what to do every time a required field failed the validation.
    },
    customValidation: { // min and max are for the length of the inputs for most fields, but are for the value of birthdate.
      first_name: {
        min: 1,
        max: 50,
        required: true,
        regex: /^[^0-9]+$/
      },
      last_name: {
        min: 1,
        max: 50,
        required: true,
        regex: /^[^0-9]+$/
      },
      full_name: {
        min: 1,
        max: 50,
        required: true,
        regex: /^[^0-9]+$/
      },
      birthdate: {
        min: '1911-01-01',
        max: '2011-12-31',
        required: true,
        regex: /^[\d\s\+\-]{4}-[\d\s\+\-]{2}-[\d\s\+\-]{2}$/
      },
      email: {
        min: 1,
        max: 50,
        required: true,
        regex: /^[\w+.-]+@([\w+.-]+\.)+[A-Za-z]{2,6}$/
      },
      phone: {
        min: 5,
        max: 20,
        required: true,
        regex: /^[\d\s\+\-]{5,20}$/
      },
      address: {
        min: 1,
        max: 200,
        required: true,
        regex: /./
      }
    }
  };
```
