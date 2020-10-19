---
title: "Handling internal URL parameters"
date: 2018-06-14
tags: [web development]
---

Yesterday I tweeted this<blockquote class="twitter-tweet" data-lang="en" data-dnt="true"><p lang="en" dir="ltr">Dear Twitter: IMO changing URL parameters manually is not a use case and I will not go the extra mile in my application to handle those cases. Discuss! ;-)</p>&mdash; Daniel Rosendorf (@drosendorf) <a href="https://twitter.com/drosendorf/status/1006807933185937408?ref_src=twsrc%5Etfw">13. Juni 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

and got some answers and questions from colleagues, so I decided to elaborate a bit.

In our current project we build a web application that supports regional instances. For this to work correctly, the user selects a country during registration and immediately gets redirected to the instance corresponding to his selected country if necessary. The instance we redirect to lives under another (sub-)domain, so we are providing the already selected country as a URL parameter. This avoids that the user has to select the country again after the redirect.

We have two links on this page which depend on the selected country. So on each country change which does not trigger an instance redirect, we trigger an event that updates those link targets. This event is normally not triggered when the URL parameter in the navigation bar is changed after the page is already loaded. My coworker added a few lines of code to handle this case as well (he is a very thorough person ;-) ). 

And this is the point I want to talk about ...

I would not have done this, simply because manually changing the parameter in the URL is not a relevant use case. The parameter is a technical detail which helps us make the application work as expected. To be clear: I have no problem with the few extra lines of code (they are in there and they will stay) and they will probably save us a few extra support cases. But if you are meddling with the URL parameters in my web application, you are doing something that you should not do and therefore I won't spent any time on helping you with this.

P.S. In any case you should validate URL parameters as any other user provided input to ensure the security of your application!
