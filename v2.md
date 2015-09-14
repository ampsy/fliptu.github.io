---
layout: default
---

# Ampsy API v2

## https://ampsy.com back-end

### GET /api/v2/campaigns/:id/posts.json

Doesn't require access token. Accepts the following parameters:

* `provider` - one of facebook, twitter, instagram, youtube, tumblr, flickr. Returns posts imported from the specified provider only.
* `timestamp` - used for pagination. Returns posts after the given value.

Returns posts from the given campaign:
{% highlight json %}
[{"id": 329806435,
  "kind": "image",
  "created_at": "2015-09-08T09:53:20Z",
  "timestamp": "1441706000000_0329806435",
  "source_url": "http://instagram.com/p/7XYNUSnrRv/",
  "social_id": "1069429904780473455_14651964",
  "social_network": "instagram",
  "media_width": 640,
  "media_height": 640,
  "media_url": "https://scontent.cdninstagram.com/hphotos-xaf1/t51.2885-15/e35/11848915_1602697673326743_153140263_n.jpg",
  "image_url": "https://scontent.cdninstagram.com/hphotos-xaf1/t51.2885-15/s320x320/e35/11848915_1602697673326743_153140263_n.jpg",
  "thumb_url": "https://scontent.cdninstagram.com/hphotos-xaf1/t51.2885-15/s150x150/e35/11848915_1602697673326743_153140263_n.jpg",
  "caption": "#Repost @mskellybrannigan with @repostapp.\n・・・\nGoodnight LA @RochelleBrodin #RochelleBrodinPhotography @treatsmag @treatswhiteparty 💋nice to run into you #gorgeous @jessegolden",
  "author": {"username": "rochellebrodin",
             "url": "http://instagram.com/rochellebrodin",
             "name": "•rOchelle•brOdin•",
             "avatar_url": "https://igcdn-photos-h-a.akamaihd.net/hphotos-ak-xaf1/t51.2885-19/s150x150/11330755_716969961768287_1368860020_a.jpg"},
  "imported": true},
 {"id": 329768311,
  "kind": "video",
  "created_at": "2015-09-08T07:59:25Z",
  "timestamp": "1441699165000_0329768311",
  "source_url": "https://instagram.com/p/7XLK5_qC2L/",
  "social_id": "1069372564501441931_180747570",
  "social_network": "instagram",
  "media_width": 500,
  "media_height": 500,
  "media_url": "http://api.embed.ly/1/video?width=500&height=500&mp4=https%3A%2F%2Fscontent.cdninstagram.com%2Fhphotos-xaf1%2Ft50.2886-16%2F11898964_1664352733781620_1508190450_n.mp4&poster=https%3A%2F%2Fscontent.cdninstagram.com%2Fhphotos-xfa1%2Ft51.2885-15%2Fe15%2F11909381_882492231817373_222996789_n.jpg&schema=instagram",
  "image_url": "https://scontent.cdninstagram.com/hphotos-xfa1/t51.2885-15/s320x320/e15/11909381_882492231817373_222996789_n.jpg",
  "caption": "These guys killed it tonight by producing such a great event @experiencenve @bretthyman @treatsmag #TreatsWhiteParty @maliburockyoaks thank you!!",
  "author": {"avatar_url": "https://scontent.cdninstagram.com/hphotos-xta1/t51.2885-19/11137600_1588330394775745_2027507912_a.jpg",
             "name": "Steve Shaw 🇬🇧📷",
             "url": "http://instagram.com/steveshawphotos",
             "username": "steveshawphotos"},
  "imported": true},
 {"id": 329766241,
  "kind": "image",
  "created_at": "2015-09-08T06:46:56Z",
  "timestamp": "1441694816000_0329766241",
  "source_url": "https://twitter.com/statuses/641140647257206784",
  "social_id": "641140647257206784",
  "social_network": "twitter",
  "media_width": 640,
  "media_height": 640,
  "media_url": "http://pbs.twimg.com/media/COXKBY8VAAADXF6.jpg:large",
  "image_url": "http://pbs.twimg.com/media/COXKBY8VAAADXF6.jpg:small",
  "thumb_url": "http://pbs.twimg.com/media/COXKBY8VAAADXF6.jpg:thumb",
  "caption": "We love @treatsmagazine. best times at #treatswhiteparty. http://t.co/EK9o61K6Cd",
  "author": {"username": "sarahtk",
             "url": "http://twitter.com/sarahtk",
             "avatar_url": "http://pbs.twimg.com/profile_images/636400182117056512/uTR2mDkY_normal.jpg",
             "name": "Sarah Tither-Kaplan"},
  "imported": true}]
{% endhighlight %}
