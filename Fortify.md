# Background

The ldng-ui-web application is the customer facing application that the users interact with through the browser. The application running on the browser is a single-page application built primarily using the Backbone JS library. The backend is a Java Spring application that exposes REST endpoints that accept and return JSON data.

# Input Validation

The application has several data entry forms; validation of data entered on the forms goes through a validation check on the browser and and on the server. On the browser, validation is handled by a Backbone plugin called backbone-forms. On the backend, endpoint validation is performed by the com.fanniemae.ldng.ui.json.model.validator.ModelValidatorNG class. The validation rules are defined in /ldng-ui-web/src/main/resources/ldng-ui-validations.properties and is shared by the Browser application and the Server.

The application allows import of XML files that contain loan information. The files go through Schema validation and custom validation defined by files in the folder /ldng-ui-web/src/main/resources/validation.

The application accepts HTML input from the user to be stored and displayed. The CKEditor JavaScript component is used to provide a rich editor for authoring HTML in the browser. On the server, the OWASP HTML sanitizer Java library is used to clean the input of unnecessary HTML entities.    

# Data display

The Backbone JS application on the Browser uses Handlebars templates to display JSON data returned from the server. The data is escaped by default before displaying. The HTML escaping section in this page explains this - http://handlebarsjs.com/

Example template file - ldng-ui-web\src\main\webapp\app\modules\all\settings\user_profile\views\templates\userProfileDetail\template.userContact.hbs 
