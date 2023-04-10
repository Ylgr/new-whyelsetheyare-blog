---
layout: blog
title: "Security smart contract - Chapter 4: Maintain"
date: 2023-04-10T13:28:42.321Z
top_image: /images/uploads/104835805_p0.jpg
tags:
  - smart-contract-security
categories:
  - Smart contract
---
After development phrase is go production time. Like other system development, maintainer is needed to make sure everything working smoothly in control. Actually, you don't want to be exploit your bussiness by some MEV and don't have any menthod to revert it. This chapter, we will find out some way to make it.

<!-- more -->

# OpenZeppelin Defender

First reason to use it, it is free ... for some feature can be used. Its still a good feature for both of maintainers and users. Here is these five: Admin, Relay, Autotasks, Sentinel and Logging. The best benefit of using OpenZeppelin Defender is they can combine to each other to optimize use case.

## Admin

Mostly, this feature will be used by maintainers and developers, it helps them manage ownership and execute authority's rights of Smart contract (for execute some sensitive function for example).

To using all supported features of this components you need to use OpenZeppelin library like governance, access control or upgradeable proxy.

Talk about upgradable, this may be the sensitive part of Smart contract when it like a knife, both protect smart contract from vulnerability and make it become vulnerability. When combine it with relay feature, it helps the upgrade ability now will be distribute between maintainers and even advance user when they can propose upgrade code version. This ensures that the upgrading process is more transparent and less susceptible to a single point of failure or misuse.