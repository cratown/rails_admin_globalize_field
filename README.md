# RailsAdminGlobalizeField

  RailsAdminGlobalizeField adds tabbed interface to [rails_admin](https://github.com/sferik/rails_admin) for multilingual models (using [globalize3](https://github.com/svenfuchs/globalize3) gem)

  It creates custom field type for globalize3 translations that you can use on any translations asssociation to translated models.

  This gem uses Translation models generated by globalize3, so you don't need to add any additional models to your project (as some older globalize3 gists suggested).

## Installation

> rails-4.0 compatible only for now!

Add and configure globalize3 gem first. **You need to use rails4 branch.**
``` ruby
  gem 'paper_trail', github: 'airblade/paper_trail'
  gem 'globalize3', github: 'svenfuchs/globalize3', branch: 'rails4'
```


Add this line to your application's Gemfile:
``` ruby
    gem 'rails_admin_globalize_field'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rails_admin_globalize_field

## Usage

Add `accepts_nested_attributes_for` for translations to your **translated** model
``` ruby
  class Model < ActiveRecord::Base
    translates :title, :desc
    accepts_nested_attributes_for :translations, :allow_destroy => true
  end
```

Configure your **translated** model to use `:globalize_tabs` field type for `translations` association:
``` ruby
  config.model 'Model' do
    edit do
      configure :translations, :globalize_tabs
    end
  end
```

Add configuration to associated **translation** model:
``` ruby
  config.model 'Model::Translation' do
    configure :locale, :hidden
    include_fields :locale, :title, :desc
  end
```
`:locale` field is always required.



## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
