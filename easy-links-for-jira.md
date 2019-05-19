---
layout: minimal
title: Easy Links for JIRA
description: Manage your JIRA issue links in an user-friendly custom field
image: '/assets/img/easy-links-for-jira/easylinks-logo.png'
searchable: true
---
![get the PDF]({{ site.url }}/assets/img/easy-links-for-jira/easylinks-logo.png "Easy Links for JIRA")
# Easy Links for JIRA

## Content

* [Introduction](#introduction)
* [How does it work?](#how-does-it-work)
* [FAQs](#faqs)
* [EULA](#eula)

## Introduction

[Easy Links for JIRA](https://marketplace.atlassian.com/plugins/com.codedpoetry.easylinks.easy-links/server/overview) provides a new customfield type that allows the user to select (single or multiple) issues in an easy, fast way. Using this custom field, the user will create/remove issue links depending on the selected options. Also, the "Linked Issue" custom field can be used in JQL functions and dashboard gadgets.

![get the PDF]({{ site.url }}/assets/img/easy-links-for-jira/usage-example.png "An EasyLinks field example")

## How does it work?

When you create an EasyLinks field, you configure it to "represent" a regular JIRA issue link type. This way, when you edit the values of the field, what EasyLinks does behind the scenes is to create/remove issue links of the configured link type for you, depending on the selected values. Also, in configuration you can restrict with a JQL expression the available values that the users can select when editing an EasyLinks field.

![get the PDF]({{ site.url }}/assets/img/easy-links-for-jira/configuration.png "Configuring EasyLinks fields")

The EasyLinks fields work like a kind of "calculated" field, if the issue already has linked issues, they will appear in the custom field value.


## FAQs

#### I have two EasyLinks fields for "blocked by" issues, but when I edit one of them, the other field changes too

Notice that when you create a custom field of this type, you configure it to be "connected" to an Issue Link Type (for example: "blocked by"). It works more or less like a calculated field: its value depends on the existing links of the configured type, BUT, when you set the value of the field, it creates (or deletes, if the value is set to "none") a new issue link with the new value. If you have more than one field that are configured to use the same issue link type, those fields will conflict and they both will be creating and updating links of the same type, so they will always show the same data (because they both will create a link of the same type, so second field will always overwrite the first one). The short conclusion of all of this is that there is a restriction: you cannot use multiple fields on the same issue link type, the workaround is to create another link type to be used by the second field.

#### I have an EasyLinks field with a JQL restriction for its value, but I can see that some issues show values that doesn't match that JQL

The JQL restriction only applies when editing the field, it just "filters" the options that the user can select. If you manually create an issue link (with the standar JIRA link dialog), EasyLinks will show it as a value of the field.

## EULA
See [EasyLinks for Jira - EULA]({{ site.url }}/easy-links-eula)
