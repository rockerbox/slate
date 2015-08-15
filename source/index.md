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
  - api/_sequential_url_pattern_search

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

We need to add authorization to all of these services and remove the advertiser parameter from the API.

We will be reusing our authentication and just need to label the endpoints are authenticated in python with the appropriate decorator.

### Cookie-based

### Header-based

# On-site Activity 

These APIs allow us to search for a particular pattern or group of patterns that occur on the query string of the on-page url. 
The search APIs give us the ability to look at the following characterstics about a patterns:

- URLs: these are the URLs that match the pattern
- UIDs: these are the UIDs that match the pattern
- Count: this gives us a summary about the pattern
- Timeseries: this gives us a timeseries summary about how the pattern changes over time





