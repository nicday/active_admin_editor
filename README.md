# Active Admin Editor

[![Build Status](https://travis-ci.org/ejholmes/active_admin_editor.png)](https://travis-ci.org/ejholmes/active_admin_editor)

This is a wysiwyg html editor for the [Active Admin](http://activeadmin.info/)
interface using [wysihtml5](https://github.com/xing/wysihtml5).

![screenshot](https://dl.dropbox.com/u/1906634/Captured/6V2rZ.png)

## Installation

Add the following to your `Gemfile`:

```ruby
gem 'active_admin_editor'
```

And include the wysiwyg styles in your `application.css`:

```css
//= require active_admin/editor/wysiwyg
```

Then run the following to install the default intializer:

```bash
$ rails g active_admin:editor
```

## Usage

This gem provides you with a custom formtastic input called `:html_editor` to build out an wysihtml5 enabled input.
All you have to do is specify the `:as` option for your inputs.

**Example**

```ruby
ActiveAdmin.register Page do
  form do |f|
    f.inputs do
      f.input :title
      f.input :content, as: :html_editor
    end

    f.buttons
  end
end
```

## Uploads

The editor supports uploading of assets directly to an S3 bucket. Edit the initializer that
was installed when you ran `rails g active_admin:editor`.

```ruby
ActiveAdmin::Editor.configure do |config|
  config.s3_bucket = '<your bucket>'
  config.aws_access_key_id = '<your aws access key>'
  config.aws_access_secret = '<your aws secret>'
  # config.storage_dir = 'uploads'
end
```

Then add the following CORS configuration to the S3 bucket:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <CORSRule>
        <AllowedOrigin>*</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedMethod>POST</AllowedMethod>
        <AllowedMethod>GET</AllowedMethod>
        <AllowedMethod>HEAD</AllowedMethod>
        <MaxAgeSeconds>3000</MaxAgeSeconds>
        <ExposeHeader>Location</ExposeHeader>
        <AllowedHeader>*</AllowedHeader>
    </CORSRule>
</CORSConfiguration>
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

### Tests

Run RSpec tests with `bundle exec rake`. Run JavaScript specs with `bundle
exec rake konacha:serve`.
