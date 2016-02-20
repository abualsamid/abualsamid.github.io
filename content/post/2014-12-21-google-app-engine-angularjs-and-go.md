---
author: abualsamid
comments: true
date: 2014-12-21 21:45:18+00:00
layout: post
slug: google-app-engine-angularjs-and-go
title: Google App Engine, AngularJS and Go
wordpress_id: 23
categories:
- Angular
- Go
- Programming
tags:
- AngularJS
- GAE
- Go
---

I am an AWS fanboy, a member of the Amazon Partner Network, certified AWS architect, certified AWS developer and most importantly run a multi-million business on AWS. I try to keep up with everything new from AWS, attend every re:Invent and try out most new things while they are still in preview.




None the less, all those cool podcasts from [Scott Hanselman](https://twitter.com/shanselman) about easy deployments to the Azure Platform as a Service piqued my curiosity. He whips together few lines of code and then uses cli tools to fire up an Azure app. So I wanted to try few things out for myself. I have been wanting to write an AngularJS app for a while. Recently I have mentioned wanting to possibly switch from Node for our ancillary projects to Go. So why not write a Go+Angular app and deploy it on a PaaS provider to get a feel for how all those things work together.




Scott’s Azure’s podcasts is what started me thinking about all of this, but I am going to defer trying out Azure for later. I [grow up](http://blog.abualsamid.com/2014/12/out-with-the-old/) in the Microsoft eco system and have seen my fair share of their awesome demos starting with the initial ASP 1.0 “zero lines of code demo”. I have been bitten enough times by .NET, Visual Studio, Windows Update that I know how much productivity can be wasted once you get past the simple demo. Our front end and middle layers are all developed in .NET, mainly Visual C#, VB.NET and knockout. So I do not feel that simply extending my domain to Azure is challenging enough. Sure, one day, soon, I will be pushing out some apps to Azure, but not today. I have not even bothered to check if Azure supports Go.




I have tried Heroku in the past and I admire their story a ton. Orion Henry’s talk at [Hacksummit](https://hacksummit.org/live/1GSWPUYHQ) was one of faves. None the less, being acquired by Salesforce and running on AWS (which i am already very familiar with) makes it less appealing to me. Joyent is another interesting possibility. However the recent [rift in the node](http://blog.abualsamid.com/2014/12/hello-world/) community gives me a pause. 




Thus, I settled on the Google App Engine. There are other PaaS providers out there, but really if you are not an AWS, Azure, GAE, Heroku or Joyent I am not sure I want to hitch by wagon to you. Rackspace is interesting, I used to run a business on Rackspace and their fanatical service is amazing. However, there is nothing unique about their offering to pull me there. Thus, Google App Engine it is.




The challenge though is I have not done anything with Angular, Go or GAE, so where does one start? For Angular, I started with the [Angular Seed project](https://github.com/angular/angular-seed). It is a starter project for Angular put together by the Angular team so it is as good a place to start as any. I forked it on Github, cloned it on my Mac and started toying with it. After a few commands using Bower I had the app up and running, no issues.




Poking around the Internet I found out that people prefer the Angular ui router to ngRoute so I switched ngRoute out for the [ui router.](http://angular-ui.github.io/#ui-router) After updating the code to use the ui router’s way of doing things I was up and running again, so far so good. My UX skills suck, so I decided to use Bootstrap to do the heavy lifting on that front. 




I added a reference to the bootstrap css from their CDN, that was easy, but what do we do about the jQuery dependency and bootstrap’s own js files? Would they play well with Angular? After more poking around I ran into the [Angular UI bootstrap project](http://angular-ui.github.io/bootstrap/) So I decided to use that instead of trying to figure out things on my own. The less work I do as far as infrastructure and frameworks the better.




So, now I have a skeleton Angular JS project, complete with advanced routing using ui router and bootstrap using the Angular UI bootstrap project, and it is [hosted on Github](https://github.com/abualsamid/livememories) with a dev copy on my Mac. Sweet, but what about Go? I started at the [GAE’s Go page](https://cloud.google.com/appengine/docs/go/). I downloaded the SDK and installed it, everything went well with no issues, just followed the instructions. 




I played around with the sample guest book app that comes with the SDK. I ran it locally, it ran nicely. I then pushed it to the GAE and again it deployed without hitch. In few minutes I was viewing my deployed app online. It is my understanding that GAE uses LXC (Linux Containers) for the deployment which explains why it only takes few moments to spin the app up. The Sandbox environment that comes with the SDK and the GAE deployments are very impressive. I have not done anything but follow the samples thus far, but so far I am very impressed with how all of this works.




So now I have a skeleton Angular App, a skeleton go app, and a working setup for the GAE deployment but how do I get the Angular app to talk to the Go app? I could not find much on how to structure the app in this case. After a lot of toying around with it, I discovered that I do not need any Go source code in the root of the project folder for GAE to work.




So I ended up creating a src folder inside the AngularJS project, sibling to the app folder. The GO code goes inside the src folder and the Angular code stays inside the app folder, config files sit in the root folder, and we are all good.




Then it was just a matter of configuring the app.yaml to let the GAE know where everything is and how to server the AnguarJS files. 




<blockquote>

> 
> application: second-core-800  
version: 1  
runtime: go  
api_version: go1
> 
> 

> 
> default_expiration: "10m"
> 
> 

> 
> skip_files:  
- ^(.*/)?#.*#$  
- ^(.*/)?.*~$  
- ^(.*/)?.*\.py[co]$  
- ^(.*/)?.*/RCS/.*$  
- ^(.*/)?\..*$  
- ^(.*/)?\.bak$  
- node_modules
> 
> 

> 
> handlers:
> 
> 

> 
> - url: /favicon\.ico   
static_files: favicon.ico   
upload: favicon\.ico
> 
> 

> 
> - url: /api/.*  
script: _go_app
> 
> 

> 
> - url: (.*)/  
static_files: app\1/index.html  
upload: app/index\.html  
mime_type: text/html; charset=utf-8
> 
> 

> 
> - url: (/.*\.css)  
static_files: app\1  
upload: app/.*\.css  
mime_type: text/css; charset=utf-8
> 
> 

> 
> - url: (/.*\.html)  
static_files: app\1  
upload: app/.*\.html  
mime_type: text/html; charset=utf-8
> 
> 

> 
> - url: (/.*\.js)  
static_files: app\1  
upload: app/.*\.js  
mime_type: text/javascript; charset=utf-8
> 
> 

> 
>  
> 
> 
</blockquote>




 




This worked great, I can navigate directly to my app, or to index.html and I will get Angular firing up instead of the Go Handler. The trick is to configure the handlers section of the config file and the upload stanza to let GAE know which static files to upload. For good measure added node_modules to the skip file section as those are only used to run the Angular Seed project and now I am using the GAE dev server to do that.




To route to the GO REST api I created a /api mapping in the config file as shown above. The GAE does not need any GO source files to be in the root folder, so that should’ve worked, but it did not.




My confusing stemmed from the way the GAE deploys my files. The documentation clearly states that the static files (my Angular) and the GO files go into separate places. I am not sure where  that is, but my guess is that the GO code goes into a LXC container and the static files are served from a virtual directory off a massive Apache or nginx server. So I was not sure how routing would work knowing that they are being split into separate locations?




Well, it turns out that once I configured my app.yaml to route GO requests to /api all I had is to handle that route in my Go code:




<blockquote>

> 
> http.HandleFunc("/api/greeting", greeting)
> 
> 
</blockquote>




 And that’s it. It worked. Now I can do something like this in Angular and it just works:




<blockquote>

> 
> .controller('Hello', ["$scope","$http",function($scope, $http) {  
  $http  
  .get('/api/greeting')  
  .success(function(data) {  
    $scope.greeting=data;  
  })  
}]);
> 
> 
</blockquote>




The app does not do much yet, but it runs on GAE, fires up an Angular app, talks to a Go REST api and it all works well.




Now, my pattern for coding would be to 




1) code, code, code.




2) git add .




3) git commit -a




4) git push origin




5) goapp deploy




and I will have my source code committed to GitHub and my app updated on GAE. Sweet...




 




 




 
