---
layout: post
title:  "Rails Custom Validation Error"
excerpt: "<p>However, at this point, I encountered another issue. The html tags are all appearing in the form!</p>"
---
I have always dislike this kind of error message because it is so ugly.

![Rails Error 1](/assets/images/rails-custom-validation-error/rails-error-1.png)

And also this as you have to refer back to the error message to identify which field contains error.

![Rails Error 2](/assets/images/rails-custom-validation-error/rails-error-2.png)

So while looking for solutions, I found this customized error message in the [Ruby on Rails Guides](http://guides.rubyonrails.org/v2.3.11/activerecord_validations_callbacks.html#error-messages-and-error-messages-for) which will produce an error message something like this.

![Ruby Rails Error](http://guides.rubyonrails.org/v2.3.11/images/validation_error_messages.png)

I realise I have to overwrite the `ActionView::Base.field_error_proc` to achieve this customization.

```
ActionView::Base.field_error_proc = Proc.new do |html_tag, instance|
  if instance.error_message.kind_of?(Array)
    %(#{html_tag}<span class="validation-error">&nbsp;
      #{instance.error_message.join(',')}</span>)
  else
    %(#{html_tag}<span class="validation-error">&nbsp;
      #{instance.error_message}</span>)
  end
end
```

Since the guide does not specify where I should place this code, I went on searching for solutions online. [Rails Casts](http://railscasts.com/episodes/39-customize-field-error) saved me when I found out that they have an episode on this topic. I finally knew that it should be placed at the `environment.rb` file.

> Always remember to restart your server after saving your environment.rb file for changes to be shown.

However, at this point, I encountered another issue. The html tags are all appearing in the form! >.<" This is bad.

![Rails Error 3](/assets/images/rails-custom-validation-error/rails-error-3.png)

And then... I found this [StackOverflow Solution](http://stackoverflow.com/questions/4251284/raw-vs-html-safe-vs-h-to-unescape-html) which sets a boolean in string so that the string is considered as html save. So now the code looks like this 

```
ActionView::Base.field_error_proc = Proc.new do |html_tag, instance|
  if instance.error_message.kind_of?(Array)
    %(#{html_tag}<span class="validation-error">&nbsp;
      #{instance.error_message.join(',')}</span>).html_safe
  else
    %(#{html_tag}<span class="validation-error">&nbsp;
      #{instance.error_message}</span>).html_safe
  end
end
```

Errors will then be shown like this and restart the server after changes are made. To achieve the red color error, just apply some css on it, and you are done :D

![Rails Error 4](/assets/images/rails-custom-validation-error/rails-error-4.png)

