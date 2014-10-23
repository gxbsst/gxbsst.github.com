---
title: Rails 3, RSpec, Cucumber, jQuery, Devise, Mongoid, and Compass(转)
author: gxbsst
layout: post
permalink: /archives/545
aktt_notify_twitter:
  - no
qzone:
  - 'true'
post_views_count:
  - 443
views:
  - 336
categories:
  - Ruby/Ruby on Rails
---
来源:http://jimdrannbauer.com/2011/01/29/rails-3-rspec-cucumber-jquery-devise-mongoid-and-compass/

Want to build a Rails 3 app with this stuff?

Git  
RSpec  
Cucumber w/ Capybara  
Mongoid  
Devise  
CanCan  
jQuery  
Compass  
Blueprintcss  
Haml  
Sass  
Capistrano  
Passenger  
Factory Girl  
Shoulda  
metric_fu  
Here’s how.

Just A Checklist

This article is mostly written for myself so I don’t have to remember where I found all of the information. There’s nothing particularly difficult about anything here. I just like the idea of having it all in one place. I figured it might be helpful to others, so… uh… here it is.

Having said that, this is not a tutorial. I don’t explain how to do Behavior Driven Development, how to use CanCan, or why to use any of this stuff. It’s just a checklist… a detailed checklist. It would probably make a good Rails Template.

Prerequisites

The installation of MongoDB and Git are beyond the scope…

Initialize the app

In your shell:

<pre lang="c">mkdir awesome-app
cd awesome-app
git init
rails new . -T -J -O
</pre>

Create the empty directory first so that you can init an empty git repo. The -T option excludes the Test/Unit files so that we can use RSpec instead. The -J option excludes the prototype.js files so that we can use jQuery instead. The -O option excludes ActiveRecord (O is for ORM) so that we can use Mongoid instead.

Commit it:

<pre lang="c">git add .
git commit -m "initial commit"
Bundle the Gems
</pre>

Here’s the first place you need to modify files. In Gemfile:

<pre lang="ruby">source 'http://rubygems.org'
gem 'rails',    '3.0.3'
gem 'mongoid',  '2.0.0.rc.6'
gem 'bson_ext', '~> 1.2'
gem 'devise'
gem 'cancan'
gem 'jquery-rails'
gem 'passenger'
gem 'capistrano'
gem "compass", ">= 0.10.6"
gem 'haml'
group :development, :test do
  gem 'capybara'
  gem 'cucumber'
  gem 'cucumber-rails'
  gem 'database_cleaner'
  gem 'rspec'
  gem 'rspec-rails'
  gem 'shoulda'
  gem 'factory_girl_rails'
  gem 'autotest'
  gem 'launchy'
  gem 'faker'
  gem 'ruby-debug19'
  gem 'haml-rails'
  gem 'metric_fu'
end

</pre>

Then, back in your shell:

<pre lang="c">bundle install
</pre>

Commit it:

<pre lang="c">git add .
git commit -m "Added Gems"
Mongoid
</pre>

Mongoid is an ORM for MongoDB. I’ll assume you have it installed already. Dig it:

<pre lang="c"># Ignore this message if you see it since you're
# running the command it's asking for right now:

# Mongoid config not found. Create a config file at: config/mongoid.yml
# to generate one run: rails generate mongoid:config
rails g mongoid:config

</pre>

After running the mongoid generator, your app is configured to use Mongoid instead of ActiveRecord. When you generate a model, Rails will generate a Mongoid Document.

Let’s edit some files and get it set up.

In config/mongoid.yml:

<pre lang="c">defaults: &#038;defaults
  host: localhost
  # mongoid defaults for configurable settings
  autocreate_indexes: false
  allow_dynamic_fields: true
  include_root_in_json: false
  parameterize_keys: true
  persist_in_safe_mode: false
  raise_not_found_error: true
  reconnect_time: 3
development:
  &lt;&lt;: *defaults
  database: awesome_app_development
test: &#038;TEST
  &lt;&lt;: *defaults
  database: awesome_app_test
cucumber:
  &lt;&lt;: *TEST
# set these environment variables on your prod server
production:
  host: &lt;%= ENV['MONGOID_HOST'] %>
  port: &lt;%= ENV['MONGOID_PORT'] %>
  username: &lt;%= ENV['MONGOID_USERNAME'] %>
  password: &lt;%= ENV['MONGOID_PASSWORD'] %>
  database: &lt;%= ENV['MONGOID_DATABASE'] %>
</pre>

There are 2 things to notice here. First, the configurable settings can be excluded. Even though Mongoid will default to the above options, leave them so that you don’t have to look at the documentation. Second, we added an environment for Cucumber which just points back to the test environment.

Commit it:

<pre lang="c">git add .
git commit -m "Added Mongoid"
RSpec
</pre>

Now, we use the rails generator to install RSpec. Shell:

<pre lang="c">rails g rspec:install
Next, in spec/spec_helper.rb:

RSpec.configure do |config|
  config.mock_with :rspec

  require 'database_cleaner'

  config.before(:suite) do
    DatabaseCleaner.strategy = :truncation
    DatabaseCleaner.orm = "mongoid"
  end

  config.before(:each) do
    DatabaseCleaner.clean
  end
end
</pre>

This is all you need in your RSpec configuration to use it with Mongoid. MongoDB doesn’t do transactions so we need to truncate the database between tests instead of rolling back. DatabaseCleaner helps with that.

Commit it:

<pre lang="c">git add .
git commit -m "Added RSpec"
</pre>

Cucumber

Next, we use the rails generator again to install Cucumber. Shell:

<pre lang="c">rails g cucumber:install --capybara --rspec --skip-database
</pre>

The –capybara option sets up Capybara instead of Webrat. The –rspec option enables RSpec matchers for your step definitions.

The Cucumber generator will bark at you about a missing database.yml file without the –skip-database option because we skipped the ORM when we created the app.

Like RSpec, some configuration is necessary to make Cucumber play nice with Mongoid. Add this file, features/support/database_cleaner.rb:

<pre lang="c">require 'database_cleaner'
DatabaseCleaner.strategy = :truncation
DatabaseCleaner.orm = "mongoid"
Before { DatabaseCleaner.clean }
</pre>

This does the same thing for Cucumber that it does for RSpec: truncates your data between scenarios.

Commit it:

<pre lang="c">git add .
git commit -m "Added Cucumber"
</pre>

Devise

Devise is used for authentication.

Shell it:

rails g devise:install  
Devise needs a few things in place so that it can provide it’s functionality and it’ll let you know it when the installation is done:

<pre lang="c">===============================================================================

Some setup you must do manually if you haven't yet:

  1. Setup default url options for your specific environment. Here is an
     example of development environment:

       config.action_mailer.default_url_options = { :host => 'localhost:3000' }

     This is a required Rails configuration. In production it must be the
     actual host of your application

  2. Ensure you have defined root_url to *something* in your config/routes.rb.
     For example:

       root :to => "home#index"

  3. Ensure you have flash messages in app/views/layouts/application.html.erb.
     For example:

       <p class="notice">
  &lt;%= notice %>
</p>
       

<p class="alert">
  &lt;%= alert %>
</p>

===============================================================================
</pre>

For now, all you need to do are steps 1 and 2 above. We’ll handle step 3 when we get into the Haml/Sass/Compass stuff later.

In config/environments/development.rb, add this:

<pre lang="c">config.action_mailer.default_url_options = { :host => 'localhost:3000' }
</pre>

In config/routes.rb, add this:

<pre lang="c">root :to => "home#index"
<pre>

Finally, Devise needs a model to hold login credentials. Let’s call it User. In the shell:
<pre lang="c">

rails g mongoid:devise User
</pre>


<p>
  Take a look in app/models/user.rb. Notice that it generated a Mongoid Document.
</p>


<p>
  Finish up by adding this to routes.rb:
</p>


<pre lang="c">

devise_for :users
Commit it:

git add .
git commit -m "Added Devise"
</pre>


<p>
  CanCan
</p>


<p>
  CanCan does role-based user authorization.
</p>


<pre lang="c">

rails g cancan:ability
That’s it.
</pre>


<p>
  Commit it:
</p>


<pre lang="c">

git add .
git commit -m "Added CanCan"
</pre>


<p>
  jQuery
</p>


<p>
  We used the -J option when we created the app so that we could use jQuery instead of Prototype. In your shell, run the jQuery generator:
</p>


<pre lang="c">

rails g jquery:install --ui
</pre>


<p>
  This’ll do 3 main things: remove the existing protoypejs-based javascript files (which, in our case, aren’t there anyway), drop in the latest jQuery, and drop in the jQuery version of the Rails Unobtrusive Javascript (UJS) Adapter. Since jQueryUI is pretty cool too, we drop that in too with the –ui option.
</p>


<p>
  In order to make the :defaults argument to javascript_include_tag load the .js files in the right order, we need to modify config/application.rb. Look for:
</p>


<pre lang="c">

config.action_view.javascript_expansions[:defaults] = %w()
and change it to:

config.action_view.javascript_expansions[:defaults] =
  %w(jquery.min jquery-ui.min rails)
</pre>


<p>
  Notice that we load the minified versions which were downloaded by the generator.
</p>


<p>
  Commit it:
</p>


<pre lang="c">

git add .
git commit -m "Added jQuery"
Compass/Haml/Sass/Blueprintcss
</pre>


<p>
  Haml is a template langauge like erb. When we added “gem ‘haml’” to the Gemfile, we made Rails recognize that files with the .haml extension contain Haml markup. Sass is a superset of css3 that helps keep your stylesheets clean. Blueprintcss is a css framework that provides easy to use reset, grid, and typographical styles. Compass ties all this together and provides a way to integrate it into your app.
</p>


<p>
  Run this to install Compass into your app using Blueprintcss:
</p>


<pre lang="c">

compass init rails . --using blueprint/semantic
</pre>


<p>
  Compass will ask you a few questions. Just say yes to both of them.
</p>


<pre lang="c">

Compass recommends that you keep your stylesheets in app/stylesheets
  instead of the Sass default location of public/stylesheets/sass.
  Is this OK? (Y/n) Y

Compass recommends that you keep your compiled css in public/stylesheets/compiled/
  instead the Sass default of public/stylesheets/.
  However, if you're exclusively using Sass, then public/stylesheets/ is recommended.
  Emit compiled stylesheets to public/stylesheets/compiled/? (Y/n) Y

</pre>


<p>
  After that, it’ll drop a bunch of files into the app and finish up with some instructions. We’ve already done the first suggestion, added Compass to the Gemfile. The second suggestion gives us the opportunity to put together our layout.
</p>


<p>
  Create app/views/layout/application.html.haml and place this inside:
</p>


<pre lang="c">


!!! XML
!!!
%html
  %head
    %title Awesome App
    = javascript_include_tag :defaults
    = csrf_meta_tag
    = stylesheet_link_tag :all
    = stylesheet_link_tag 'compiled/screen.css', :media => 'screen, projection'
    = stylesheet_link_tag 'compiled/print.css',  :media => 'print'
    /[if lt IE 8]
      = stylesheet_link_tag 'compiled/ie.css', :media => 'screen, projection'

  %body.bp.two-col

    #container

      #header
        %h1 Awesome App Header

      #sidebar
        %div item 1
        %div item 2
        %div item 3
        %div item 4

      #content

        %p.notice= notice
        %p.error= alert
        %p.success= notice

        = yield

      #footer
        %h3 Awesome App Footer

</pre>


<p>
  There are a few things to notice in there. First, it’s Haml. Second, we’ve included the stylesheet info from the compass command output in the head. Third, we’re using the built-in Blueprintcss 2-column layout. Finally, we’ve added the notice and alert elements that Devise asked for earlier. There’s also a success element in there to show off some of the coloring that Blueprintcss gives you.
</p>


<p>
  If you try to look at it now, it won’t work. Sit tight, we’re close.
</p>


<p>
  Making Compass Just Work
</p>


<p>
  The Compass documentation seems to lack a simple explanation of how to see if things just work. Here it is:
</p>


<p>
  Create app/stylesheets/partials/_application.scss, and place this inside:
</p>


<pre lang="c">

#container {
  @include showgrid;
}
</pre>


<p>
  Use this file to get started adding your own styles. The showgrid mixin is useful for debugging your Blueprintcss grid. Delete it or comment it out when you’re done.
</p>


<p>
  Then, add this to app/stylesheets/screen.scss:
</p>


<p>
  // Add the application styles.<br />
  @import "partials/application";<br />
  This makes sure that your own styles are available when you get around to adding them.
</p>


<p>
  Commit it:
</p>


<p>
  git add .<br />
  git commit -m "Added Compass"<br />
  Last Steps Before Starting the App
</p>


<p>
  Delete public/index.html:
</p>


<p>
  rm public/index.html<br />
  Earlier, Devise instructed us to setup the root route in routes.rb. The problem is the route we added won’t actually work until we have a home controller with an index action.
</p>


<p>
  Shell it:
</p>


<p>
  rails g controller home index<br />
  Notice that the views generated use Haml. That works because we added the ‘haml-rails’ gem to the Gemfile.
</p>


<p>
  Then, so that we can see Devise in action:
</p>


<p>
  rails g controller vip index<br />
  In app/controllers/vip_controller.rb, add:
</p>


<p>
  before_filter :authenticate_user!<br />
  Commit it:
</p>


<p>
  git add .<br />
  git commit -m "Added Home and Vip controllers and views"<br />
  Start It Up
</p>


<p>
  passenger start<br />
  Now go to: http://localhost:3000
</p>


<p>
  Nice! See the grid? Clean.
</p>


<p>
  How about this one? http://localhost:3000/vip/index
</p>


<p>
  Go ahead. Mess with the login stuff. It’ll just kinda work.
</p>


<p>
  One More Thing, metric_fu
</p>


<p>
  Add this to your Rakefile:
</p>


<p>
  require 'metric_fu'<br />
  MetricFu::Configuration.run do |config|<br />
    config.rcov[:test_files] = ['spec/**/*_spec.rb']<br />
    config.rcov[:rcov_opts] << "-Ispec" # Needed to find spec_helper<br />
  end<br />
  Get your metrics by running this:
</p>


<p>
  rake metrics:all<br />
  Commit it:
</p>


<p>
  git add .<br />
  git commit -m "Added metric_fu"<br />
  Conclusion
</p>


<p>
  Okay, so it doesn’t really do anything… yet. That’s okay. You’re smart. Make.
</p>


<p>
  There were a few things in the list at the top that I didn’t go into more detail about (Capistrano, Passenger, Factory Girl, and Shoulda). That’s because they’re ready to go; inclusion in the Gemfile was enough. Just start using ‘em.
</p>


<p>
  Links
</p>


<p>
  Here’s a list of links to the documentation and articles I used to pull this together:
</p>


<p>
  http://relishapp.com/rspec/rspec-rails
</p>


<p>
  http://github.com/aslakhellesoy/cucumber-rails/blob/master/README.rdoc
</p>


<p>
  http://github.com/thoughtbot/shoulda
</p>


<p>
  http://github.com/thoughtbot/factory_girl_rails
</p>


<p>
  http://mongoid.org/docs/installation
</p>


<p>
  http://mongoid.org/docs/integration
</p>


<p>
  http://mongoid.org/docs/extensions
</p>


<p>
  http://github.com/plataformatec/devise
</p>


<p>
  https://github.com/ryanb/cancan
</p>


<p>
  http://www.tonyamoyal.com/2010/07/28/rails-authentication-with-devise-and-cancan-customizing-devise-controllers/
</p>


<p>
  https://github.com/indirect/jquery-rails
</p>


<p>
  http://haml-lang.com/
</p>


<p>
  http://sass-lang.com/
</p>


<p>
  http://compass-style.org/
</p>


<p>
  http://blueprintcss.org/
</p>


<p>
  https://github.com/joshuaclayton/blueprint-css/wiki
</p>


<p>
  转载请注明：<a href="http://www.weixuhong.com">韦旭红的点点滴滴</a> &raquo; <a href="http://www.weixuhong.com/archives/545">Rails 3, RSpec, Cucumber, jQuery, Devise, Mongoid, and Compass(转)</a>
</p>