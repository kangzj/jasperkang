---
title: Example of Sending SMS in PHP Using AWS SNS
tags:
  - AWS
  - php
  - SMS
  - SNS
id: 2035
categories:
  - Others
date: 2016-12-29 10:39:07
---


<pre class="lang:php decode:true " >$client = AWS::createClient('Sns');
$sms = [
	'Message' =&gt; 'sms_content',
	'PhoneNumber' =&gt; 'sms_recipient',
	'MessageAttributes' =&gt; [
		'AWS.SNS.SMS.SenderID' =&gt; [
			'DataType' =&gt; 'String',
			'StringValue' =&gt; 'AD'
		],
		'AWS.SNS.SMS.SMSType' =&gt; [
			'DataType' =&gt; 'String',
			'StringValue' =&gt; 'Transactional'
		],
	]
];
$result = $client-&gt;publish($sms);</pre>
