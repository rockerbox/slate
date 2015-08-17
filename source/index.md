---
title: API Reference

language_tabs:
  - shell
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - api/url_search
  - api/multiple_url_search
  - api/sequential_url_pattern_search

  - errors


search: true
---

# Crusher

Crusher allows you to look at the on-site activity user and determine how the on-site activity is influenced by a users off-site browsing activity.
These are the APIs that power crusher and make it possible to analyze on-site versus off-site activity.

## Background

Crusher is a collection of analytics, machine learning and ad-buying technologies that make it possible for a user to: 

- collect information about on-site and off-site activity
- classify and understand how these behaviors influence each other
- target ads based on these different classifications 

## Important Terms

These are standard terms that are used when referring to different components within crusher. 
They allow us to use common language when thinking about how different pieces of crusher are related to on another.

### Event

An event is an atomic unit of interaction on an advertisers website. Currently this is limited to page views and conversions but may expand in the future to include javascript triggered events such as expanding images, scrolling, etc. 

### Action

An action is a group of events that are all related to the same functionality. For instance, an action may be used to describe all landing pages, even though the individual url for each landing page is different. 

### Funnel

A funnel is a group of actions that occur (often sequentially) that is used to predict a goal. For instance, a user that visits a landing page, a product page and converts would represent a funnel.

# Authentication

## Authorization

Most of our APIs require authentication. We demonstrate here how to login using cookie-based authentication.

### Cookie-based

> Use the `/login` endpoint, saving your cookie in a file to use for future requests

```shell
curl -b cookie -c cookie -X POST -d '{"username": "my_user", "password": "my_pw"}' "portal.getrockerbox.com/login"
```

To log in using the cookie-based authentication, send a `POST` request to `portal.getrockerbox.com/login` with an object containing the username and password assigned to you by Rockerbox. 

You'll need to have cookies enabled in order to use your credentials in future requests. If using curl, use the `-b` and `-c` options to read/write your cookie from disk.

### Header-based

Rick doesn't like APIs that don't have this as an option, so we're going to make this a thing...at some point.

### Permissions

> Request

```shell
curl -b cookie -c cookie "portal.getrockerbox.com/account/permissions"
```

> Response

```json
{
    "results": [
        {
            "external_advertiser_id": 987654,
            "pixel_source_name": "examle_advertiser_1",
            "advertiser_name": "Example Advertiser One",
            "selected": true
        },
        {
            "external_advertiser_id": 123456,
            "pixel_source_name": "example_advertiser_2",
            "advertiser_name": "Example Advertiser Two",
            "selected": false
        }
    ]
}
```

Once authenticated, you can use `/account/permissions` to view the advertisers you have access to.

# On-site Activity 

These APIs allow us to search for a particular pattern or group of patterns that occur on the query string of the on-page url. 
The search APIs give us the ability to look at the following characterstics about a patterns:

- URLs: these are the URLs that match the pattern
- UIDs: these are the UIDs that match the pattern
- Count: this gives us a summary about the pattern
- Timeseries: this gives us a timeseries summary about how the pattern changes over time





