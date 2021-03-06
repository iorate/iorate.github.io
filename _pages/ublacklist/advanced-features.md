---
permalink: /ublacklist/advanced-features
title: Advanced Features
---

## Rules

You can edit rules to block sites in the options page, as well as in the "Block this site" dialog.

![rule editor](/assets/images/ublacklist/advanced-features/rules-1.png)

You can write rules by [match patterns](#match-patterns) or [regular expressions](#regular-expressions).

### Match patterns

Match patterns are URLs including wildcards. You can see the details in [MDN web docs](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Match_patterns).

Here are examples of **valid** match patterns.

|Pattern|Example matches|
|`*://example.com/*`<br><br>(URLs hosted at `example.com`)|`http://example.com/`<br><br>`https://example.com/hoge`|
|`*://*.example.net/*`<br><br>(URLs hosted at `example.net` or its subdomain)|`http://example.net/`<br><br>`https://foo.example.net/hoge`|
|`*://example.org/hoge/*`<br><br>(URLs hosted at `example.org` and whose path starts with `/hoge/`)|`http://example.org/hoge/fuga.html`|

Here are examples of **invalid** match patterns.

|Invalid pattern|Reason|
|`*://www.qinterest.*/`|`*` is not at the start. Use [regular expressions](#regular-expressions) instead.|
|`<all_urls>`|Not supported.|

### Regular expressions

You can write more flexible rules by [regular expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions).

Note that regular expression rules shall be regular expression **literals** in JavaScript, surrounded by `/` (e.g. `/example\.(net|org)/`).

Here are examples of **valid** regular expressions.

|Regular expression|Example matches|
|`/^https:\/\/www\.qinterest\./`<br><br>(URLs starting with `https://www.qinterest.`)|`https://www.qinterest.com/`<br><br>`https://www.qinterest.jp/hoge`|
|`/^https?:\/\/([^/.]+\.)*?xn--/`<br><br>(URLs including internationalized domain names)|`http://例.テスト/`|

Here are examples of **invalid** regular expressions.

|Invalid regular expressions|Reason|
|`^https?:\/\/example\.com\/`|Not surrounded by `/`.|
|`/^https?://example\.com//`|Inner `/` are not escaped.|

### Unblock rules

Match patterns or regular expressions preceded by `@` mean that the specified sites are not blocked.

They can be used to unblock sites that are blocked by [subscriptions](#subscription). For example, if `http://example.com/` is blocked by a subscription, you can unblock it by `@*://example.com/*`.

## Other search engines

This extension supports [Bing](#bing), [DuckDuckGo](#duckduckgo), [Ecosia](#ecosia) (partially) and [Startpage.com](#startpagecom). This feature is disabled by default and can be enabled in the options page.

![other search engines](/assets/images/ublacklist/advanced-features/other-search-engines-1.png)

### Bing

![bing](/assets/images/ublacklist/advanced-features/bing.png)

### DuckDuckGo

![duckduckgo](/assets/images/ublacklist/advanced-features/duckduckgo.png)

### Ecosia

For now, search scopes other than "Web" (e.g. "Images" and "Videos") are not supported.

![ecosia](/assets/images/ublacklist/advanced-features/ecosia.png)

### Startpage.com

![startpage](/assets/images/ublacklist/advanced-features/startpage.png)

## Sync

You can synchronize blacklists among devices using Google Drive or Dropbox.

<p class="notice--warning">
<strong>NOTE:</strong> For technical reasons, sync is not available in Firefox for Android.
</p>

To turn on sync, click the "Turn on sync" button in the options page and select a cloud.

![turn on sync](/assets/images/ublacklist/advanced-features/sync-1.png)

Follow the instructions on the dialog to authenticate.

![authenticate](/assets/images/ublacklist/advanced-features/sync-2.png)

Once authentication succeeds, your blacklist will be regularly synchronized with the selected cloud.

### Google Drive

If you use Firefox or its derivative, you will be required to permit access to `https://www.googleapis.com`.

The blacklist is saved in the application data folder on your Google Drive. It is hidden from you, although you can delete it in the settings page of Google Drive.

### Dropbox

The blacklist is saved in the `/Apps/uBlacklist/` folder on your Dropbox. The folder name may be different depending on your language.

## Subscription

You can subscribe to public blacklists.

To add a subscription, click the "Add subscription" button and enter the name and URL. You will be required to permit access to the origin of the URL.

![add subscription](/assets/images/ublacklist/advanced-features/subscription-1.png)

You can show, update or remove a subscription.

![manage subscription](/assets/images/ublacklist/advanced-features/subscription-2.png)

### Publish a subscription

To publish a blacklist as a subscription, place a blacklist file encoded in UTF-8 on a suitable HTTP(S) server, and publish the URL.

It is a good idea to host your subscription on GitHub. Make sure that you publish the **raw** URL ([example](https://raw.githubusercontent.com/iorate/ublacklist-example-subscription/master/uBlacklist.txt)).

![raw url](/assets/images/ublacklist/advanced-features/subscription-3.png)
