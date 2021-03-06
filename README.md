# WooCommerce Subscriptions - Post Trial Fee

## Background
This started as a demo WooCommerce plugin for twitch stream. Then it moved on to be a feature plugin for WooCommerce and WooCommerce Subscriptions. 


## Description

WC Subscriptions has a Sign-Up fee that is a one time fee, but it is not possible to charge this after the parent order.
This plugin adds a "Post Trial Fee" to Simple and Variable subscriptions. The fee is added to the first renewal after a Free trial.
 


## Goal 1

Default functionality of WooCommerce and WooCommerce Subscriptions 
is to charge Sign-up Fee with first order and not first renewal.

1. Example for Subscription with 5 day free trial, $0 Sign-up fee, $45 per month.

Order | Amount
----|---
Parent Order| $0
First renewal | $45
Second renewal | $45

2. Example for Subscription with 5 day free trial, $8 Sign-up fee, $45 per month.

Order | Amount
----|---
Parent Order| $8
First renewal | $45
Second renewal | $45

3. Custom functoionality desired for Subscription with 5 day free trial, $8 Sign-up fee, $45 per month.

Order | Amount
----|---
Parent Order| $0
First renewal | $45 + $8
Second renewal | $45

Proposed solution:

- Add "Post Trial Fee" field to Product Data
- When Parent Order is placed
	add meta_key   = "_add_fee"
	    meta_value = "true"
- Hook into Renewal Process 
	if (_add_fee)
		add fee from field ($8)
		delete_meta( _add_fee )
