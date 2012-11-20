# Devise Masquerade

[![Build Status](https://secure.travis-ci.org/oivoodoo/devise_masquerade.png?branch=master)](https://travis-ci.org/oivoodoo/devise_masquerade)

It's a utility library for enabling functionallity like login as button for
admin.

If you have multi users application and sometimes you want to test functionally
using login of existing user without requesting the password, define login as
button with url helper and use it.

## Installation

Add this line to your application's Gemfile:

    gem 'devise_masquerade'

And then execute:

    $ bundle

## Usage

In the view you can use url helper for defining link:

    = link_to "Login As", masquerade_path(user)

Add into your application_controller.rb:

    before_filter :masquerade_user!

Instead of user you can use your resource name admin, student or another names.

## Custom controller for adding cancan for authorization

    class Admin::MasqueradesController < Devise::MasqueradesController
      def show
        authorize!(:masquerade, User)

        super
      end
    end

## Custom url redirect after masquerade:

    class Admin::MasqueradesController < Devise::MasqueradesController
      def show
        authorize!(:masquerade, User)

        super
      end

      protected

      def after_masquerade_path_for(resource)
        "/custom_url"
      end
    end

## You can redefine few options:

    Devise.masquerade_param = 'masquerade'
    Devise.masquerade_expires_in = 10.seconds
    Devise.masquerade_key_size = 16 # size of the generate by SecureRandom.base64

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
