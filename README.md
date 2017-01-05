# Rails application with client_side_validations.

This RoR application is an example of using [client_side_validations](https://github.com/DavyJonesLocker/client_side_validations) in pair with [devise](https://github.com/plataformatec/devise).

My steps (commits):

* Create Rails application. I am using rails 5.0.1 and ruby 2.3.1 versions. [29ba33c](https://github.com/sorefull/front_end_validation/commit/29ba33cbd09bad46f1585cdf3b41b22c08cf88b7)

* Creating User model via devise gem [a4207c3](https://github.com/sorefull/front_end_validation/commit/a4207c3e06012e99cc2b92f243ec23b606642956)

  [devise instructions](https://github.com/plataformatec/devise#getting-started)

  Also I generated views and created some useful links like 'log out', 'sign up' and 'log in' in application layout.

* Installing gem client_side_validations [5271ac4](https://github.com/sorefull/front_end_validation/commit/5271ac4ccb51eb6aca8c5c688e8f11d77b6d5ec6)

  [Installing](https://github.com/DavyJonesLocker/client_side_validations#install),
  [Setting](https://github.com/DavyJonesLocker/client_side_validations#usage)

  If you are using Rails 5 and got this `DEPRECATION WARNING: alias_method_chain is deprecated` warning [here](https://github.com/DavyJonesLocker/client_side_validations/issues/645) is issue. I used it.

  After installing and setting config file `config/initializers/client_side_validations.rb` will be generated.

  ```ruby
  # ClientSideValidations Initializer

  # Disabled validators. The uniqueness validator is disabled by default for security issues. Enable it on your own responsibility!
  # ClientSideValidations::Config.disabled_validators = [:uniqueness]
  ClientSideValidations::Config.disabled_validators = []

  # Uncomment to validate number format with current I18n locale
  # ClientSideValidations::Config.number_format_with_locale = true

  # Uncomment the following block if you want each input field to have the validation messages attached.
  #
  # Note: client_side_validation requires the error to be encapsulated within
  # <label for="#{instance.send(:tag_id)}" class="message"></label>
  #
  ActionView::Base.field_error_proc = Proc.new do |html_tag, instance|
    unless html_tag =~ /^<label/
      %{<div class="field_with_errors">#{html_tag}<label for="#{instance.send(:tag_id)}" class="message">#{instance.error_message.first}</label></div>}.html_safe
    else
      %{<div class="field_with_errors">#{html_tag}</div>}.html_safe
    end
  end

  ```

  I've set disabled_validators = [] to try ajax uniqueness front end validation. And it works perfectly. Uncommented lines 15-21 to see validation messages in form.

## Summary

This gem is a simple way to validate models on client side. It supports additional FormBuilders, custom validation and views.
