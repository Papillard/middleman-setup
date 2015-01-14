## Advanced Front-End

--

## HTML is a poor language

- You can't repeat HTML code (by looping)
- You can't inject HTML code in other pages
- You have to copy/paste your code in different pages (**hard to maintain**)

### BUT SADLY

Your browser speaks only HTML

--

## Templates are powerful

Templating languages come with

- **layout** system
- **partial** system
- **looping** structures

<br>

**Many choices**: liquid, handlebar, **ERB**.

All must be **processed to pure HTML**

--

## CSS is a poor language

- No variable to store widths, heights, colors...
- No functions, no nesting of selectors
- You have to copy/paste CSS rules, your design is not **consistent**.

### BUT SADLY

Your browser **speaks only CSS**

--

## SASS is powerful

- You can define **variables**
- You can define **functions or mixins**
- You can **nest selectors**
- Your design is consistent and your code DRY

<br>

See http://sass-lang.com/guide

SASS must be **processed to pure CSS**


---

## Advanced front-end setup

![]({% asset_path setup/middleman.png %})

[Middleman](http://middlemanapp.com/) = front-end framework which allows sass and templates.

--

## Create new site

```
$ middleman init my-site
$ cd my-site
```

Launch your server with

```
$ middleman server
```

**`Ctrl + C`** to kill the server

--

## Switch to scss

- We want SCSS, not CSS
- Get rid of all the **.css files** in **`stylesheets`**
- Replace them by a new file **`all.css.scss`**


```
└── stylesheets
    └── all.css.scss (notice the .scss extension)
```

--
## Integrate front-end libraries

- Popular front-end libraries (jQuery, Bootstrap, etc..) all have **gems**.
- These gems will install **js**, **css**, **scss** files on your computer.
- You can **import** these files **without putting them physically** in your project.

--
## Installation

```ruby
# Gemfile
gem 'jquery-middleman'
gem 'bootstrap-sass', '~> 3.3.1'
gem 'font-awesome-sass', '~> 4.2.0'
```

```scss
// source/stylesheets/all.css.scss
@import "bootstrap";
@import "font-awesome-sprockets";
@import "font-awesome";
```

```javascript
// source/javascripts/all.js
//= require jquery
//= require bootstrap-sprockets
//= require_tree .
```

```
$ bundle install
```

--

## Documentation

- https://github.com/jasl/jquery-middleman
- https://github.com/twbs/bootstrap-sass
- https://github.com/FortAwesome/font-awesome-sass

--

## Viewport for Responsiveness

Don't forget these lines in layout for Bootstrap responsiveness

```erb
<!-- source/layouts/layout.erb -->
<head>
  <!-- [...] -->
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <%= stylesheet_link_tag "all" %>
  <!-- [...] -->
</head>
```

--
## Deployment setup

```ruby
# Gemfile
gem 'middleman-deploy', '~> 1.0'
```

```ruby
# config.rb
activate :deploy do |deploy|
  deploy.method = :git
  # Optional Settings
  # deploy.remote   = 'custom-remote' # remote name or git url, default: origin
  # deploy.branch   = 'custom-branch' # default: gh-pages
  # deploy.strategy = :submodule      # commit strategy: can be :force_push or :submodule, default: :force_push
  # deploy.commit_message = 'custom-message'      # commit message (can be empty), default: Automated commit at `timestamp` by middleman-deploy `version`
end
```

```
$ bundle install
```

--
## Deployment commands

Compile and test your website locally in a `build` folder

```
$ middleman build
```

Deploy the `build` folder on gh-pages
```
$ middleman deploy
```
