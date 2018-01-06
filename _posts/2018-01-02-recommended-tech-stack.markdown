---
layout: post
title:  "2018 My AWS Web Tech Stack"
date:   2018-01-06 06:05:08 -0800
categories: best tech stack, best web tech stack, aws tech stack, fullstack aws, full stack aws, aws stack, aws, web tech stack
description: With the start of 2018, I'd like to share my favorite web tech stack for AWS. This stack is excellent for web applications of any kind - user facing platforms, sass products, api-driven webservices and more. If you're looking for a tech stack, here's a great place to start.
---

With the seemingly infinite amount of web tech stacks available to developers today,
I thought it best to share my preferred web programming stack.
I've split this post into four sections -
Frontend Programming, Frontend Infrastructure, Backend Programming and Backend Infrastructure.
I also link to relevant videos that will get you started with this stack.
Almost every component of this tech stack has relevant tutorials on the [Youtube Channel]({{ site.youtube_channel_url }}).
Let's dig in!

<h3>Frontend Programming</h3>
I look for these attributes in a modern frontend stack.
1. Easy installation
2. Fast live reload for quick iteration cycles
3. Easy deployment
4. Simple yet extensible syntax

All of these come out of the box with [create-react-app](https://github.com/facebookincubator/create-react-app). I'm in love with create-react-app.
It is my all time favorite developer experience. Assuming npm is installed on your developer machine,
creating and running a new project requires three commands:
"npm install -g create-react-app", "create-react-app my-app && cd my-app", "npm run start"

CSS styles reload without refreshing the page, so styling an app made with create-react-app is very easy.
Markup and Javascript changes reload usually in a second or two. This means I spend hardly any time
waiting for my changes to compile, and almost all of my time adding valuable features to my projects. Though the makers
of create-react-app recommend using pure css for most applications, sometimes developers will require
the power of sass. [Here's how to include sass in your create-react-app.](https://www.youtube.com/watch?v=B_zZDa80FVo)

Deploying is also simple. create-react-app comes with a built-in npm script: "npm run build" which will bundle
everything up for an easy deployment to AWS S3 which is covered under the infrastructure section below.

While conceptually JSX might seem alien to a traditional web programmer, working with it becomes very intuitive
after a few days of practice. React is a simple yet extremely powerful frontend view layer framework, perfect for
the presentation layer of a website. A react component can be as simple as a pure function that takes a single props
argument and returns JSX that describes the HTML markup to render. React is also blazingly fast, has a top notch
community behind it with awesome tutorials everywhere,
[and has a minified size of 34.8 kb gzipped as of version 16.0](https://reactjs.org/blog/2017/09/26/react-v16.0.html#reduced-file-size) which helps
websites load faster, especially for ever-increasingly important mobile device users.

P.S. I recommend performing proprietary business logic in your backend software,
and using frontend projects for presentation only. This will help safeguard your intellectual property and make
it easier to get away with using less rigid model and controller layers for the frontend like those offered by Angular.

Also see: [Why I prefer React over Angular](/react/vs/angular/4,/why/is/awesome,/use/react,/angular,/overview/2018/01/05/2018-topics.html)

<h3>Frontend Infrastructure</h3>
I deploy frontend projects to AWS S3 and use Cloudfront as a CDN and for HTTPS. AWS S3 is super cheap. Cloudfront
caches assets stored in AWS S3, and delivers theme over HTTPS through its CDN. HTTPS is a necessity for modern
websites, and an important factor in keeping your users safe on the web. This infrastructure is super cheap, fast
and secure.

See [Deploying a React App with AWS S3](https://www.youtube.com/watch?v=rVj3zc30-8E) and [HTTPS for an AWS S3 Static Website using Cloudfront](https://www.youtube.com/watch?v=_Jw6tHUp6js&t=82s) for video tutorials.

<h3>Backend Programming</h3>
My backend stack varies on a case by case basis. A lot of the time I will write a
dashboard / CRUD application using Symfony and, if necessary, interface with microservices written in
NodeJS or Scala that handle processes requiring higher load. For most readers, I expect Symfony will
be enough. Optionally add NodeJS or Scala as you see fit. I try to keep everything as stateless as possible
so horizontal scaling can be applied in the future.

I use [PHP & Symfony](http://symfony.com/at-a-glance) with [Doctrine](https://symfony.com/doc/current/doctrine.html) if I want to build a backend for
an user-facing app with a lot of CRUD (Create, Read, Update, Delete).
I find the Symfony ecosystem to be very rigid, well-documented and uniform - which makes it great for projects with more than one developer.
The [Symfony Coding Standards](http://symfony.com/doc/current/contributing/code/standards.html#symfony-coding-standards-in-detail) are frankly
the sexiest I know of. Code written properly for Symfony is beautiful! Symfony is a fantastic beginner
framework. The only drawback of Symfony
is that it was written for PHP, which has limited (very limited) support for asynchronous programming models.
On the flip side, PHP is one of the most popular languages on the web. Finding PHP developers seems to be easier
than finding NodeJS or especially Scala developers.

I choose between either [NodeJS with Express](https://expressjs.com/)
or the [Scala Play Framework](https://www.playframework.com/) for backend projects that require
performance. Both languages support asynchronous programming models, a crucial feature when creating performant software.
I typically build these as microservices, because I find that larger NodeJS and Scala applications tend to get messy and
are hard to collaborate on.

I use NodeJS for simple microservices that I want to complete quickly, deploy, and then never touch again.
The barriers to entry for building an application with
NodeJS are very low. NodeJS runs fast, has a small executable footprint and has very limited server requirements
which makes it great for deployment with Docker. Javascript, the language of NodeJS has a very easy-to-read
syntax, and also the language of frontend programming, so frontend developers can learn NodeJS easily and visa versa.
With the advent of ES6, programming in NodeJS is expressive and fast.

Node does not have strong typing,
which opens the door to simple and sometimes hard to debug mistakes. However, the weak typing does lend itself
well to rapid development, so keep this is mind when comparing NodeJS vs Scala for your microservice.

Scala has an exceptional collections library and tools for asynchronous reactive programming. The main reason
I choose Scala over NodeJS is its strong typing, which helps with avoiding making syntactical mistakes. Scala is also
a compiled language which helps with catching errors before releasing. Most packages written for Java will
work with Scala which means it has a very large collection of 3rd party libraries available.
Last year I would have used Java in place of Scala, but I find Scala to be better
than Java in every way other than its larger learning curve.

Drawbacks of Scala Play vs Express: Scala compile time goes from bad to worse when projects get larger. The learning curve
is really, really high. I rate it as the hardest language I've ever learned. Running and deploying Scala Play requires
knowledge of the Java Virtual Machine. Scala tends to have much larger server requirements than NodeJS because of its
dependency on the JVM.

<h3>Backend Infrastructure</h3>
PHP Symfony, NodeJS Express and Scala Play all get baked into [Docker](https://docs.docker.com/get-started/) container images and deployed on
AWS EC2 Container Service. PHP Symfony is unfortunately harder to deploy because it requires both NGINX and PHP-FPM for its
server. Express is executable out of the box, so creating a Docker container for it is very simple and just
requires NodeJS installed to run. Scala Play compiles to an executable and will run in a Docker container with the correct
version of Java installed.

AWS EC2 Container Service (ECS) keeps your docker containers running for you. So once you deploy your backend services,
you can sit back, relax and let ECS take the wheel. An AWS Application Load Balancer (ALB) will round robin traffic
to as many instances of your docker containers as you like. I've got tutorials on how to deploy Symfony and Scala Play
with docker on the YouTube Channel, linked below. The ALB exposes analytics related to service health, request frequency
and response codes out of the box. Express will have a similar Docker build to Scala Play, with the main difference
being its dependency on NodeJS instead of Java.

For Symfony Deployments See:

[Building Docker Containers for PHP Symfony API](https://www.youtube.com/watch?v=W_3nbAKh860)

[Building Docker Containers for PHP Symfony API Continued](https://www.youtube.com/watch?v=N-bEXMhxmY0)

[Deploying Symfony 3 with Docker & AWS ECS](https://www.youtube.com/watch?v=1Sxw2LqJigs)

For Scala Deployment See:

[Deploying Scala Play To AWS ECS with Docker](https://www.youtube.com/watch?v=KCS8bPUtomY)

<h3>Thanks For Reading!</h3>
I hope this post helps readers with choosing a good web stack and reduces the amount of research needed
when starting a new project. This stack represents the culmination of 5 years of professional web development
experience with input from a lot of insanely smart colleagues. It's a great starting place for almost
any web project.
As always, I'm going to plug the [Youtube Channel]({{ site.youtube_channel_url }}). Subscribe if you love the content
and feedback is always appreciated. Community Discussion should happen
over at the [Channel's Discussion Page](https://www.youtube.com/channel/UCPrcrJwwcMGWpOv_qRJOuIA/discussion).

<meta name="twitter:card" content="summary">
<meta name="twitter:site" content="@codewithnate">
<meta name="twitter:creator" content="@codewithnate">
<meta name="twitter:title" content="2018 My AWS Web Tech Stack">
<meta name="twitter:description" content="With the start of 2018, I'd like to share my favorite web tech stack for AWS. This stack is excellent for web applications of any kind - user facing platforms, sass products, api-driven webservices and more. If you're looking for a tech stack, here's a great place to start.">