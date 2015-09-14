---
layout: default
---

# Fliptu API v1

## https://fliptu.com back-end

Access token should be passed as an http parameter:

* inside the url for GET requests:
{% highlight bash %}
curl 'https://fliptu.com/api/v1/overview?access_token=...'
{% endhighlight %}
* inside the url or the post body for POST requests:
{% highlight bash %}
curl -d 'access_token=...&account_id=...' https://fliptu.com/api/v1/brands/:id/accounts/:network
{% endhighlight %}
* all calls that don't require access token still use it if it's present (to determine if user has access to the flipbook or can like the flip for example)

### GET /api/v1/flipbooks/:id

Doesn't require access token.

### GET /api/v1/flipbooks/:id/flips

Doesn't require access token.

### GET /api/v1/flips/:id

Doesn't require access token.

### GET /api/v1/flips/:id/comments

Doesn't require access token.

### POST /api/v1/contact_form

Doesn't require access token, accepts name, email, text arguments, sends a message to the staff members (for custom plan requests).

### POST /api/v1/cards

Doesn't require acces token, accepts `params[:card]`: a hash with number, name, expiration_month, expiration_year, security_code values, returns a uniq card token in an id field: `{ id: '...' }`

### GET /api/v1/plans

Doesn't require access token, returns a list of all plans.

### GET /api/v1/overview

Requires access token, lists all brands user has access to:
{% highlight json %}
[{"id": "...",
  "name": "...",
  "personal": "...",
  "flipbooks": [{"id": "...",
                 "name": "...",
                 "social_page": "..."}],
  "social_networks": [{"name": "...",
                       "account_id": "..." }]}]
{% endhighlight %}

### POST /api/v1/brands/:id/accounts/:network

Requires access token, accepts account_id (unique code returned by Fliptu.social call), connects the account to the brand.

### DELETE /api/v1/brands/:id/accounts/:network

Requires access token, disconnects specified social network account from the brand.

### GET /api/v1/brands/:id/subscription

Requires access token, returns the subscription for the brand:
{% highlight json %}
{ "plan_id": "...",
  "card_number": "(the last 4 digits)",
  "feeds_used": "...",
  "feeds_extra": "(the number of extra feeds added in the admin)",
  "feeds_limit": "...",
  "card_url": "/api/v1/cards",
  "url": "/api/v1/brands/:id/subscription",
  "contact_form_url": "/api/v1/contact_form" }
{% endhighlight %}

### PUT /api/v1/brands/:id/subscription

Requires access token, accepts plan_id, card (a token from the above), promo (promo code), returns a subscription object (same as above).

### DELETE /api/v1/connect

Requires access token, removes the access token.

### POST /api/v1/brands/:id/flipbooks

Requires access token, accepts the following arguments (either as json or as regular post):
{% highlight json %}
{"data": {"kind": "(one of collection, campaign, social, crowdbook)",
          "name": "test4",
          "moderated": false,
          "open": false,
          "private": false,
          "keyword": "",
          "mention": "",
          "username": "",
          "import_from": "05/27/2015 10:35 am PDT",
          "import_until": "05/28/2015 04:31 am PDT",
          "parent_id": "(for crowdbook albums)",
          "featured_offer": null,
          "featured_offer": {"name":"test",
                             "description":"test",
                             "price":"99.99",
                             "offer_url":"test",
                             "expires_at":"05/27/2015 10:43 am PDT"},
           "location": "(for display purposes only)",
           "radius": "0",
           "address": "Champ de Mars, Eiffel Tower, 5 Avenue Anatole France, 75007 Paris, France (used only for geocoding if no geocoords specified)",
           "city": "Paris (for display purposes only)",
           "state": "Île-de-France (for display purposes only)",
           "zip": "75007 (for display purposes only)",
           "geocoords": "48.85837009999999,2.2944813000000295"}}
{% endhighlight %}
returns json representation of the flipbook's data (the same fields as above with addition of urls). Featured offers can also have an image attached - in this case only http multipart can be used, not json, the format is the same, image field should be `data[featured_offer][image]`

### PUT /api/v1/flipbooks/:id

Requires access token, updates the flipbook, arguments are the same as in flipbook creation.

### DELETE /api/v1/flipbooks/:id

Requires access token, deletes the flipbook.

### GET /api/v1/user

Requires access token, returns the current user's info:
{% highlight json %}
{"id": "...",
 "login": "...",
 "avatar": "...",
 "small_avatar": "...",
 "has_password": "(false if signed up using facebook)"}
{% endhighlight %}

## http://fliptu.com/assets/fliptu.js

### Fliptu.login(client_id, callback)

Connects fliptu account to the 3rd party app using the oauth-like flow - it opens up a fliptu login dialog with the ability to signup and login using email and facebook, recover password, etc and asks users to connect fliptu account with 3rd party app and then generates a new access token for the user/app pair and triggers the callback with that token. (for example wordpress integration app calls it like this `Fliptu.login('wordpress', function (token) { ... })` - the client_id is 'wix' and 'wordpress' for now) - and the token will be null if user cancels the connect request

### Fliptu.social(network, callback)

Adds a social account to fliptu app and returns one-time unique code in the callback, it doesn't connect the account to any brand or auth a user - it should be done using the `POST /api/v1/brands/:id/accounts/:network` endpoint from above (for example `Fliptu.social('twitter', function (accountId) { ... })`)

### Fliptu.importBrands(access_token, callback)

Asks to grant manage pages permission: opens a new window with 'import brands' button which triggers facebook login - if fliptu user identified by the `acces_token` already has a facebook account and currently logged in facebook user is not that account, then alert is displayed; if user doesn't grant manage_pages permission, alert is displayed; if everything is ok then `callback` is triggered with `{ success: true }`
