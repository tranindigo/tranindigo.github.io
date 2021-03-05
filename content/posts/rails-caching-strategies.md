---
title: "Rails Caching Strategies"
date: "2020-08-25"
categories: 
  - "optimization"
  - "ruby"
  - "ruby-on-rails"
---

Rails comes packaged with three types of caching techniques: page caching, action caching, and fragment caching. We'll shortly talk about each strategy to better understand them.

#### Page caching

Page caching allows the generated page to be fulfilled by the webserver without ever having to go through the Rails stack at all. This is very fast, but you can't use it in every situation, such as pages that need authentication, and you'll also have to deal with cache expiration as well. To enable page caching, you'll need to use the `caches_page` method in your controller. Keep in mind that page caching ignores all query parameters. For instance, `/foo?page=1` will be written to the filesystem as `foo.html` with no reference to the `page` parameter. If someone requests `/foo?page=2`, they will get the cached version of page 1. You can get around this problem by using path parameters instead of query parameters.

#### Action caching

Action caching allows the incoming request to go from the web server to the Rails stack. This allows authentication and other restriction to be run while serving the result of the output from a cached copy. To enable action caching, you'll need to add  `caches_action :<method_name>` to your controller. If your page contains dynamic elements, such as your user's name or email), you can render the layout dynamically while still caching the action's contents. You can do this by using `layout: false`. You can use `expire_action` to remove the action from your cache when new data is written.

#### Fragment caching

Fragment caching allows us to cache different parts of a page so that we can cache and expire them differently. This allows a fragment of view logic to be wrapped in a cache block and served out of the cache store when the next request comes in. The following code, for example, will cache the name of all pasta products that we have in an online grocery store:

```html
<% cache("cache_key") do %>
  <p>Our pasta products</p>
  <% Pasta.all.each do |p| %>
    <%= link_to p.name, inventory_url(p) %>
  <% end %>
<% end %>
```

#### Low-level caching

You can use `Rails.cache` to directly cache any information that needs to be cached at the atomic level. This is useful to store data that is costly, such as database queries or API calls.

The best way to implement low-level caching is to use `Rails.cache.fetch`. This method will read the value from the cache. If the value is not available in the case of a cache miss, it will execute a block passed to it. The return value of the block will be written to the cache under the given cache key, and that return value will be returned.

```ruby
Rails.cache.fetch("cache_key") do
  Pasta.all
end
```
