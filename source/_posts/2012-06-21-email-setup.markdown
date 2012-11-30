---
layout: post
title: "我的电子邮件设置"
---

对于一个[终端控](https://twitter.com/chenshaoju/status/211147259738464256)来说，[对着浏览器是很难写出字来的](https://twitter.com/dingdeng/status/215134994618789888)。但是这个星球上最好的电子邮件服务 Gmail 却偏偏是基于浏览器的。我可以在终端下通过 [IMAP](http://en.wikipedia.org/wiki/Internet_Message_Access_Protocol) 协议操作 Gmail，但是在线的 IMAP 操作，特别是在网络连接不稳定的情况下，太痛苦了。经过一段时间的摸索以及较长时间的试用，我逐渐形成了这样的电子邮件使用模式：

*   所有邮件都汇总到 Gmail 做过滤、分类与搜索。
*   使用 IMAP 协议定时跟 Gmail 同步邮件，并在本地起一个邮件服务器提供 IMAP 服务。
*   简单邮件在 Gmail 里处理，需要长篇大论的邮件在连接了本地邮件服务器的客户端里处理。

下面是一些细节。

## 汇总邮件到 Gmail

Gmail 可以[代收](http://support.google.com/mail/bin/answer.py?hl=en&ctx=mail&answer=21288)其他邮箱的邮件，也可以[代发](http://support.google.com/mail/bin/answer.py?hl=en&ctx=mail&answer=22370)，所以只要邮箱还在网上，都很好处理。麻烦的是已经通过 [POP](http://en.wikipedia.org/wiki/Post_Office_Protocol) 协议收到本地的邮件，特别是当本地使用的还是很邪门的存储形式（比方说 [nnml](http://www.gnus.org/manual/gnus_194.html)）的时候。好在 nnml 虽然跟谁都不兼容，但内容好歹还是纯文本的。我网上找了个[脚本](http://www.enyo.de/fw/scripts/nnml2maildir.pl)（Perl 脚本，点击会自动下载），就把邮件目录转成了 [Maildir](http://cr.yp.to/proto/maildir.html) 形式。

剩下的就是把转出来的 Maildir 同步到 Gmail，这个跟本地 IMAP 服务器与 Gmail 之间同步邮件的原理是一样的，接下来会说。

过滤、分类与搜索是 Gmail 一直以来的强项，就没有必要多说了。

## 本地 IMAP 服务器与 Gmail 的同步

本地 IMAP 服务器与 Gmail 的同步其实就是本地 Maildir 与 Gmail 的同步，因为绝大多数的 IMAP 服务器都支持 Maildir 形式的邮件存储。事实上，绝大多数的邮件客户端也都支持直接读写 Maildir。那我为什么还费这么大劲套一层 IMAP 上去呢？因为当时我还没确定用哪一个邮件客户端——之前用的是 [Gnus](http://www.gnus.org/)，但是有在考虑 [Mutt](http://www.mutt.org/)，甚至 [Notmuch](http://notmuchmail.org/)——所以我想还是把接口抽象到网络协议这个层面比较好，谁知道哪天我会不会又爱上一个只支持 IMAP 协议的客户端呢。

目前我客户端用的是 Gnus（没时间学其他的，就这还是在学校里的时候学的），本地 IMAP 服务用的是 [Dovecot](http://dovecot.org/)，邮件存储用的是 Maildir，与 Gmail 同步用的是 [OfflineIMAP](http://offlineimap.org/)。

软件的具体配置就不说了，不折腾会死星人应该都能搞定。
