+++
Title = "The Return of Static Websites"
Description = "Everything old is new again and static websites are making a comeback."
Tags = ["static", "html", "development"]
Categories = ["notes"]
Date = "2018-03-16"
+++

Everything old is new again and static websites are making a comeback. 

<!--more-->

To start, here is some ancient history. The first website I ever coded was a static `index.html`, uploaded to a server somewhere and then available for the world to see. 

Since, we've abstracted the process of creating websites to Content Management Systems. The most popular like WordPress and Drupal are dynamic systems built around a database and PHP. CMS are easy for users and allow a lot of flexibility. 

But they have key downsides. The architecture can become bloated and slow, especially for simple websites. Speed over the wire becomes an issue, especially if you are working off a slower internet connection over or on a mobile device. These sites also can be security risks, and carry a large attack surface. 

As other development tools have evolved, we've thought of ways to incorporate benefits from the CMS user experience, and combine it with the stability and security of static websites. Already these techniques are allowing large organizations to manage various levels of content. As the tools evolve, we are likely to see even more creative applications come to life. 

One of my favorite examples is [1Password], who use a static site because of the high-level of security. Their [documentation][1Password docs] site is built with [Hugo], a static site generator written in Go. It doesn't stop the site from being beautiful, fast, and clear.

There is a whole cult of these catalogued at [JAMStack], proving that branding is almost everything when it comes to reviving old web technologies. 

Because what tools like Hugo and other static site generators do is a fancy version of that first site I coded. It is the opposite of the database-driven website. 

This approach comes with a host of benefits. 

The site is faster across all contexts. Files live right on the server without needing queries to the database. Over mobile and slower connections, this can make all the difference in a site experience. 

The attack surface is drastically reduced. With no database and no PHP, there is little to try and exploit from the site architecture. The site is maintained within a file structure, easily checked and backed up regardless of server. 

So if we're not sacrificing on speed and security, what is the downside of static sites? 

It used to be that they were difficult for users to manage, and didn't offer the same kind of non-technical editing experience offered by a CMS. Their lack of dynamic content limited features like comments and real-time posting.

This is changing. Some of the new tools like [Forestry] and [NetlifyCMS] are providing graphical interfaces for static sites. Third-party services have stepped in with options to take care of the functionality seamlessly. Forms, comments, discussion boards, etc. are all easily packaged in SaaS applications. These technologies are still in their early days, but they will continue to evolve and grow. 

In cases where we may not need the full capabilities of a CMS, we should not just settle for the familiar option. In building out new sites, we should continue to evaluate the necessary features of the tools and technologies we use against their tradeoffs.

Static sites are a viable an option for many projects. Their speed and security may win the day as their ease-of-use improves with new tools. 


[1Password]: https://1password.com
[1Password docs]: https://support.1password.com/
[Hugo]: /writing/hugo
[Forestry]: https://forestry.io
[NetlifyCMS]: https://www.netlifycms.org/ 


[JAMStack]: https://jamstack.org/examples/
