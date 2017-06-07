---
title: 利用Google两步验证来增强你网站的安全性
tags:
  - google
  - Google Authentication
  - One Time Password
  - OTA
  - 一次性密码
  - 安全
  - 密码
id: 1886
categories:
  - Programming
date: 2011-12-20 17:50:23
---

密码学当中最安全的密码是一次性密码OTP（One Time Password），即每次使用的密码都不同。目前安全性要求比较高的系统，比如网上银行或公司vpn、财务等系统都使用了一些一次性密码方案，比较多的是RSA的token卡，它上面显示六位数字，每一分钟变化一次。_[YubiKey](http://yubico.com/yubikey)_、短信验证等都算是OTP的实现。

但是这些方案都需要单独一种硬件支持。对于有大量用户的网站不太实惠，要增强安全性，还需要用户花钱买一个token卡，于是Google搞了一个”身份验证器”（Google Authentication）。Google公开算法，于是我们 就可以利用它来增加我们网站的安全性了。

<!--more-->

[![3](http://blog.kangzj.net/wp-content/uploads/2011/12/3_thumb.jpg "3")](http://blog.kangzj.net/wp-content/uploads/2011/12/3.jpg)[![1](http://blog.kangzj.net/wp-content/uploads/2011/12/1_thumb.jpg "1")](http://blog.kangzj.net/wp-content/uploads/2011/12/1.jpg)[![2](http://blog.kangzj.net/wp-content/uploads/2011/12/2_thumb.jpg "2")](http://blog.kangzj.net/wp-content/uploads/2011/12/2.jpg)

wordpress可能通过这个插件来实现两步验证： http://wordpress.org/extend/plugins/google-authenticator/ ，但是rpc发布没有实现这样的功能，因为像live writer这样的工具并无这样的功能。

找到了一个类：[google2fa](http://blog.kangzj.net/wp-content/uploads/2011/12/google2fa.zip) ，可以很方便地在PHP中验证Google Authenticator用法如下：
<pre>$InitalizationKey = "WOLEGEQUXXXXXXXXXX";// Set the inital key

$TimeStamp	  = Google2FA::get_timestamp();
$secretkey 	  = Google2FA::base32_decode($InitalizationKey);// Decode it into binary
$otp       	  = Google2FA::oath_hotp($secretkey, $TimeStamp);// Get current token

echo("Init key: $InitalizationKeyn");
echo("Timestamp: $TimeStampn");
echo("One time password: $otpn");

// Use this to verify a key as it allows for some time drift.

$result = Google2FA::verify_key($InitalizationKey, "123456");

var_dump($result);</pre>