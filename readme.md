## Facebook Open Graph Meta tag for Refinery CMS.

### Installing

Add refinerycms-fb_metatag to your Gemfile

    gem 'refinerycms-fb_metatags', :git => 'git://github.com/sunil-shrestha/fb_metatag.git'

Run generator

    rails g refinery:fb_metatag

Run migration

    rake db:migrate


### Setup fb_metatag
1. Add new fb_metatag 
Create new fb-metatag from fb_metatag menu. provide appropriate model or resource name in right format. e.g : refinery/blog/post 
Default meta tags for resource can be set here. However, meta tag on provided for individual model will be used if provided
2. Render form for the page to add og metatag fields. e.g. :
	<blockquote>
	<%= render "/shared/fb_metatag" , :f => f  %>	</blockquote>
3. Add Meta tags at header of your page. i.e. :
`<% array=(params[:controller]).split('/') %>`
`<% model_name = (array.last).singularize.downcase %>`
`<% @params= instance_variable_get("@#{model_name}") %>`
<% if (params[:action]=="show") %>
<%= raw "<meta property=\"og:title\" content=\"#{@params.og_title}\"/>" %>
  <%= raw "<meta property=\"og:description\" content=\"#{@params.og_description}\"/>" %>
  <%= raw "<meta property=\"og:type\" content=\"#{@params.og_type}\"/>" %>
  <%= raw "<meta property=\"og:url\" content=\"#{request.url }\"/>" %>
  <%= raw "<meta property=\"article:tag\" content=\"#{@params.article_tag}\"/>" %>
  <%= raw "<meta property=\"article:author\" content=\"#{@params.article_author}\"/>" %>
  <%= raw "<meta property=\"og:image\" content=\"http://www.iwa.fi/images/logo.png\"/>" %>
  <% else %>
  <meta property="og:title" content="Iwa Labs Oy" />
  <meta property="og:type" content="company" />
  <meta property="og:url" content="<%= request.url %>" />
  <meta property="og:image" content="http://www.iwa.fi/images/logo.png" />
  <meta property="og:site_name" content="Iwa Labs" />
  <meta property="fb:app_id" content="212311028070" />
  <meta itemprop="name" content="Iwa Labs Oy" />
  <meta itemprop="description" content="" />
  <meta itemprop="image" content="http://www.iwa.fi/images/logo.png" />
  <% end %>`
4. Restart your application: This gem adds og attributes when you add the model to fb_metatag. So it requires restart of application to take it in to affect.


### License

Copyright 2013 Iwa Labs Ltd. Licensed under the MIT License.
