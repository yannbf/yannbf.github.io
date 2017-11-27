---
title: "How to make a transparent header on Ionic 2"
date: 2017-03-16T05:58:00.000Z
---

{{< figure src="https://yannbraga.com/wp-content/uploads/2017/03/Transparent-header-Banner.png" class="center" link="/posts/how-to-transparent-header-ionic2/" >}}

Have you ever tried to customize your app header on ionic 2? What about making it transparent? I have, and I can say it took me a long time to realise how simple this was. At first I was able to achieve the transparency effect by using some hackish css...<!--more--> but it wasn't really the prettiest solution (imagine a bunch of<em> !important </em>all around). It took me a while but I found out that the ionic team had already created wonderful properties that do all the work for you. This is what I will be showing you today.
<!--more-->

Recently this topic was brought up on Ionic slack community, and I thought: <em>Why not write about it? It might save some people a few good hours of research</em>. If you haven't heard of this community, it's made of over <strong>11 thousand </strong>developers and designers that discuss all kinds of things about ionic 1 and 2. You should definitely <a href="http://ionicworldwide.herokuapp.com/">join us!</a>

ANYHOW. ¯\_(ツ)_/¯

<iframe src="//giphy.com/embed/l3vRimg8c7ssGb172" width="480" height="269" frameborder="0"></iframe>

## Getting started
Note: Before starting this tutorial, make sure you have the latest ionic and cordova installed. If you do not have it, make sure to <a href="https://nodejs.org/en/">install node</a> then run on your terminal:
<pre><span class="gp">$ </span>npm install -g ionic cordova</pre>
## Have everything you need? Let's do it.

First, create your project structure:
<pre>$ ionic start transparentHeaderDemo --v2 sidemenu<br/>
$ cd transparentHeaderDemo</pre>

Right after that, let's add a background image to our main page by accessing our <span style="color: #e04343;">pages/page1/page1.scss</span> file and adding the following code:


{{< highlight go>}}
page-page1 {
  ion-content {
    background-image: url('https://images.pexels.com/photos/107958/pexels-photo-107958.jpeg?w=940&h=650&auto=compress&cs=tinysrgb');
    background-size: cover;
    background-position-x: 50%;
  }
}
{{< /highlight >}}



Now we have a beautiful background that'll help us see the transparency effect. From now on, I'll be showing how the app looks on android (on the left) and ios (on the right):

<div style="text-align: center">
  <img src="https://yannbraga.com/wp-content/uploads/2017/03/Selection_170.png" />
</div>

Let's add some content by going to <span style="color: #e04343;">pages/page1/page1.html </span>and adding the following code:


{{< highlight go>}}
<ion-header>
  <ion-navbar>
    <button ion-button menuToggle>
      <ion-icon name="menu"></ion-icon>
    </button>
    <ion-title>Page One</ion-title>
  </ion-navbar>
</ion-header>
<ion-content padding>
  <ion-card>
    <img src="https://images.pexels.com/photos/2156/sky-earth-space-working.jpg?w=940&h=650&auto=compress&cs=tinysrgb" />
  </ion-card>
  <ion-card>
    <img src="https://images.pexels.com/photos/24895/pexels-photo-24895.jpg?w=940&h=650&auto=compress&cs=tinysrgb" />
  </ion-card>
  <ion-card>
    <img src="https://images.pexels.com/photos/87651/earth-blue-planet-globe-planet-87651.jpeg?w=940&h=650&auto=compress&cs=tinysrgb"/>
  </ion-card>
  <ion-card>
    <img src="https://images.pexels.com/photos/23789/pexels-photo.jpg?w=940&h=650&auto=compress&cs=tinysrgb" />
  </ion-card>
  <ion-card>
    <img src="https://images.pexels.com/photos/2159/flight-sky-earth-space.jpg?w=940&h=650&auto=compress&cs=tinysrgb" />
  </ion-card>
</ion-content>
{{< /highlight >}}


Which will give us the following result:
<div style="text-align: center">
  <img src="https://yannbraga.com/wp-content/uploads/2017/03/Selection_171.png" />
</div>

Ok, so now we have enough content to scroll and it's time to customize that header. As I told you before, the framework already has built in properties that do all the work. All you gotta do is add the <strong>transparent</strong> input property to your <strong>ion-navbar</strong>. Yes, that simple. What took me a chunk of css ended up as just a simple word in a component:


{{< highlight go>}}
<ion-header>
  <ion-navbar transparent>
    <button ion-button menuToggle>
      <ion-icon name="menu"></ion-icon>
    </button>
    <ion-title>Page One</ion-title>
  </ion-navbar>
</ion-header>
{{< /highlight >}}


Also, add a some small stylings just to make the header title and button white:

{{< highlight go>}}
page-page1 {
  ion-content {
    background-image: url('https://images.pexels.com/photos/107958/pexels-photo-107958.jpeg?w=940&h=650&auto=compress&cs=tinysrgb');
    background-size: cover;
    background-position-x: 50%;
  }
  .bar-buttons,
  .toolbar-title {
    color: #fff;
  }
{{< /highlight >}}


With that we achieve this nice result:

<div style="text-align: center">
  <img src="https://yannbraga.com/wp-content/uploads/2017/03/Selection_174.png" />
</div>

But wait, there's a weird line on my android app! See the red arrow pointing at it? Yes, by default, all headers on android have a box-shadow effect. This may be sometimes useful, even when using transparent headers, but let's remove it for now. To do so, all we have to do is add another input property, <strong>no-border</strong>, to our <strong>ion-header</strong>:

{{< highlight go>}}
<ion-header no-border>
  <ion-navbar transparent>
    <button ion-button menuToggle>
      <ion-icon name="menu"></ion-icon>
    </button>
    <ion-title>Page One</ion-title>
  </ion-navbar>
</ion-header>
{{< /highlight >}}


Which finally leads us to what we want:

<div style="text-align: center">
  <img src="https://yannbraga.com/wp-content/uploads/2017/03/Selection_175.png" />
</div>

Great! Look at what we have so far:

<div style="text-align: center">
  <img src="https://yannbraga.com/wp-content/uploads/2017/03/Transparent-Header.gif" />
</div>

Wait! Isn't the header supposed to be fully transparent? Why is the content not being shown as I slide it up?

This happens because the default behavior of a header on ionic is to not overlay content. Don't worry though, if you want to achieve that, there's another input property that helps us achieve that: <strong>fullscreen</strong>. This one you add on <strong>ion-content</strong>:

{{< highlight go>}}
<ion-header no-border>
  <ion-navbar transparent>
    <button ion-button menuToggle>
      <ion-icon name="menu"></ion-icon>
    </button>
    <ion-title>Page One</ion-title>
  </ion-navbar>
</ion-header>
<ion-content fullscreen padding>
  // code goes here..
</ion-content>
{{< /highlight >}}

And there you have it! A nice transparency effect on your header:

<div style="text-align: center">
  <img src="https://yannbraga.com/wp-content/uploads/2017/03/Fullscreen-Transparent-Header.gif" />
</div>

## To sum up
This is the final code used in this tutorial:
<h6>page1.html</h6>

{{< highlight go>}}
<ion-header no-border>
  <ion-navbar transparent>
    <button ion-button menuToggle>
      <ion-icon name="menu"></ion-icon>
    </button>
    <ion-title>Page One</ion-title>
  </ion-navbar>
</ion-header>
<ion-content fullscreen padding>
  <ion-card>
    <img src="https://images.pexels.com/photos/2156/sky-earth-space-working.jpg?w=940&h=650&auto=compress&cs=tinysrgb" />
  </ion-card>
  <ion-card>
    <img src="https://images.pexels.com/photos/24895/pexels-photo-24895.jpg?w=940&h=650&auto=compress&cs=tinysrgb" />
  </ion-card>
  <ion-card>
    <img src="https://images.pexels.com/photos/87651/earth-blue-planet-globe-planet-87651.jpeg?w=940&h=650&auto=compress&cs=tinysrgb"/>
  </ion-card>
  <ion-card>
    <img src="https://images.pexels.com/photos/23789/pexels-photo.jpg?w=940&h=650&auto=compress&cs=tinysrgb" />
  </ion-card>
  <ion-card>
    <img src="https://images.pexels.com/photos/2159/flight-sky-earth-space.jpg?w=940&h=650&auto=compress&cs=tinysrgb" />
  </ion-card>
</ion-content>
{{< /highlight >}}


<h6>page1.scss</h6>
{{< highlight go>}}
page-page1 {
  ion-content {
    background-image: url('https://images.pexels.com/photos/107958/pexels-photo-107958.jpeg?w=940&h=650&auto=compress&cs=tinysrgb');
    background-size: cover;
    background-position-x: 50%;
  }
  .bar-buttons,
  .toolbar-title {
    color: #fff;
  }
}
{{< /highlight >}}

Yet a simple change, this can be <em>a great improvement</em> and add a lot of value to your app. This was my first tutorial for ionic2 ever written, and I hope you liked it and I hope it saves you time as it would have saved mine. Feel free to leave some feedback, make requests or do whatever else you want on the comments section.

See you next time!