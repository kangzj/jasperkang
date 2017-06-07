---
title: 博客升级到wordpress2.8.1(20090720 升级到wordpress 2.8.2)
tags:
  - php
  - wordpress
id: 267
categories:
  - Blogging
date: 2009-07-11 10:12:04
---

    直接就给在线升级了，下面是官方的change-log:
<!--more-->
WordPress 2.8.1 fixes [many bugs](http://core.trac.wordpress.org/query?status=closed&amp;group=resolution&amp;order=priority&amp;milestone=2.8.1&amp;resolution=fixed) and tightens security for plugin administration pages. [Core Security Technologies](http://corelabs.coresecurity.com/index.php?module=FrontEndMod&amp;action=list&amp;type=advisory) notified us that admin pages added by certain plugins could be viewed by unprivileged users, resulting in information being leaked. Not all plugins are vulnerable to this problem, but we advise upgrading to 2.8.1 to be safe.

What else is new since 2.8?  Read through the highlights below, or  [view all changes since 2.8](http://core.trac.wordpress.org/log/branches/2.8/?action=stop_on_copy&amp;mode=stop_on_copy&amp;rev=11699&amp;stop_rev=11553&amp;limit=500)

*   Certain themes were calling get_categories() in such a way that it would fail in 2.8\. 2.8.1 works around this so these themes won’t have to change.
*   Dashboard memory usage is reduced.  Some people were running out of memory when loading the dashboard, resulting in an incomplete page.
*   The automatic upgrade no longer accidentally deletes files when cleaning up from a failed upgrade.
*   A problem where the rich text editor wasn’t being loaded due to compression issues has been worked around.
*   Extra security has been put in place to better protect you from plugins that do not do explicit permission checks.
*   Translation of role names fixed.
*   wp_page_menu() defaults to sorting by the user specified menu order rather than the page title.
*   Upload error messages are now correctly reported.
*   Autosave error experienced by some IE users is fixed.
*   Styling glitch in the plugin editor fixed.
*   SSH2 filesystem requirements updated.
*   Switched back to curl as the default transport.
*   Updated the translation library to avoid a problem with mbstring.func_overload.
*   Stricter inline style sanitization.
*   Stricter menu security.
*   Disabled code highlighting due to browser incompatibilities.
*   RTL layout fixes.
引自：[http://wordpress.org/development/2009/07/wordpress-2-8-1/](http://wordpress.org/development/2009/07/wordpress-2-8-1/)