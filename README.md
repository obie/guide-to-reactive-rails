# Guide to Reactive Rails
This repository aims to briefly introduce the concept and showcase helpful content that may help you on your Reactive Rails journey. Watch this repository to stay up to date on the latest information published on the web about Reactive Rails. (Contributions welcome, just send a PR.)

## What is Reactive Rails?

_Reactive Rails_ is a term used to describe a particular design philosophy or architectural style of web application development using Ruby on Rails. The style sits in the middle of a hypothetical continuum having RESTful (aka "vanilla") HTML server-rendered apps on one extreme, and Rails API + React or other front-end framework single-page applications (SPA) on the other.

Reactive Rails empowers small teams of full-stack Rails developers to produce rich, real-time user experiences with server-rendered HTML and minimal Javascript. It honors the motivating spirit of the Ruby on Rails framework, which is to allow small teams to do big things, while being unabashedly inspired by [Phoenix LiveView](https://github.com/phoenixframework/phoenix_live_view), a competing web framework written in Elixir.

### Why is it called "Reactive"?

Reactive Rails enables fast asynchronous _reaction_ to user events, which is something that until recently has only been possible with the use of front-end frameworks such as React or Angular. Typical server-rendered page requests take a minimum of at least 100-500 ms to process, and when you take into account the time that the browser needs for re-rendering the screen using the HTML payload sent from the server, the request cycle is often measured in whole seconds.

In Reactive Rails apps, user interactions are passed to the server over websockets instead of normal HTTP requests. Lightweight handlers change application state on the server, then the current page is automatically re-rendered and sent back to the browser. DOM diffing is used to change the screen to reflect the new application state without having to re-render the whole document. In best case scenarios, the screen can be updated in 20-30ms. Page refreshes under 200-300ms are generally considered to be imperceptible.

Another reason that the style is called "Reactive" is that when you add component-oriented view design versus just templates, as many are doing, then the design patterns that emerge begin to resemble those used to write apps in React, except of course that the dominant programming language remains Ruby, instead of Javascript.

### Reactive Rails technology stack

Reactive Rails is made possible by [ActionCable](https://guides.rubyonrails.org/action_cable_overview.html). It's also inspired, but does not necessarily require the use of [Turbolinks 5](https://github.com/turbolinks/turbolinks) and [StimulusJS](https://stimulusjs.org/).

While there are other frameworks that can be used to do reactive Rails development, the one with the most traction and momentum appears to be StimulusReflex, created by [Nate Hopkins aka hopsoft](https://github.com/hopsoft).

#### StimulusReflex
[StimulusReflex](https://docs.stimulusreflex.com/) is the main library added to Rails to make it "reactive". It is heavily inspired by StimulusJS and uses a similar syntax for hooking into browser events, except that instead of triggering actions on local Javascript-based controllers, it triggers them on the server via ActionCable channels. The reactions to those events on the server are implemented as "reflexes", a kind of lightweight controller action that is primarily concerned with mutating server state.

#### CableReady
StimulusReflex is built on top of [CableReady](https://cableready.stimulusreflex.com/), which is a wrapper around ActionCable that greately enhances its functionality, primarily by enabling direct control of the browser's DOM from the server.

#### ViewComponent
[ViewComponent](https://github.com/github/view_component) is a framework extracted from Github's main monolith application that is used to build view components that are, in their words, "reusable, testable & encapsulated". The use of view components makes reactive Rails development feel a little bit like writing React code, because of the latter's emphasis on component classes for constructing its views.

## Examples and Demos / Sample Code

[Working example apps](http://expo.stimulusreflex.com/) like Chat, Calendar, Todo, and more, with full source code.

[Toast-style alerts system](https://gist.github.com/obie/5c56d87c7b7e4e343ef7504349a69515) using [Shoelace](https://shoelace.style/)

## Videos

### The "Twitter in 10 minutes" video
Mainstream awareness (among Rails developers, anyway) of Reactive Rails was stimulated (ha!) by Hopsoft's [Build a real-time Twitter clone in 10 mins with Rails and StimulusReflex](https://dev.to/codefund/build-a-real-time-twitter-clone-10-mins-with-rails-and-stimulusreflex-5h5c) video, kind of like how Ruby on Rails original hype cycle was sparked off by DHH's [How to build a blog engine in 15 minutes](https://www.youtube.com/watch?v=Gzj723LkRJY&feature=youtu.be).

### Tutorials

Building a Reactive Todo List with Ruby on Rails 6 and Stimulus Reflex by TechmakerTV [link](https://www.youtube.com/watch?v=eK1CM0MBF64)

Episode #209 - Reactive Applications with Stimulus Reflex by DriftingRuby [link to preview](https://www.youtube.com/watch?v=K9QeC9CsYiU)

Introduction to StimulusReflex by GoRails [link](https://www.youtube.com/watch?v=gbMbGOigjA8)

Create Fast Apps With Stimulus Reflex And RailsBytes Templates In Ruby On Rails 6 by Deanin [link](https://www.youtube.com/watch?v=hxqkTy2SB78)

Stimulus Reflex Morph Modes | Selector Morphs with Rails View Components by TechmakerTV [link] (https://www.youtube.com/watch?v=bwFrjIC8wfE)

## Reading

Blog posts and other stuff that you can read.

### Documentation

[StimulusReflex Documentation](https://docs.stimulusreflex.com/)

### Introductory Blog Posts

[A future for Rails: StimulusReflex](https://headway.io/blog/a-future-for-rails-stimulusreflex) includes source for a chat app

[Reactive Rails Applications with StimulusReflex](https://dev.to/finiam/reactive-rails-applications-with-stimulusreflex-48kn)

### Tutorials

[Twitter Clone with StimulusReflex gone Hybrid Native App](https://dev.to/julianrubisch/twitter-clone-with-stimulusreflex-gone-hybrid-native-app-17fm) builds on the original Hopsoft twitter clone video by turning it into a native app. 

[Reactive Map with Rails, Stimulus Reflex and Mapbox](https://dev.to/ilrock__/reactive-map-with-rails-stimulus-reflex-and-mapbox-1po4) leverages reactive Rails to quickly build a map application.

[Infinite Horizontal Slider with CableReady and the Intersection Observer API](https://dev.to/julianrubisch/infinite-horizontal-slider-with-cableready-and-the-intersection-observer-api-4o4i)

[Lightning fast reactive action with Stimulus Reflex partial morphs](https://dev.to/rolandstuder/lightning-fast-reactive-action-with-stimulus-reflex-partial-morphs-2fg5) introduces morphing in reflexes.

[Using Tippy.js with StimulusReflex and CableReady](https://dev.to/mepatterson/using-tippy-js-with-stimulusreflex-and-cableready-3gno)

### Hype

The [excited blog post](https://medium.com/@obie/react-is-dead-long-live-reactive-rails-long-live-stimulusreflex-and-viewcomponent-cd061e2b0fe2) that I wrote when I figured out Reactive Rails is all about.

[Announcement of morph in StimulusReflex 3.3](https://dev.to/leastbad/stimulusreflex-v3-3-morphs-has-been-released-o3e) by leastbad, one of the most outspoken members of the StimulusReflex community.

## Useful Libraries

[Shoelace](https://shoelace.style/) because once you're thinking in components, using pre-packaged web components becomes a lot more appealing.

[Optimism](https://github.com/leastbad/optimism) drop-in remote form validation.

[Futurism](https://github.com/julianrubisch/futurism) lazy-load view partials.

[Turbolinks iOS Wrapper](https://github.com/turbolinks/turbolinks-ios/) is the reactive Rails answer to React Native.

[StimulusUse by Hopsoft](https://github.com/stimulus-use/stimulus-use) is a collection of composable behaviors for your Stimulus Controllers.

[StimulusControllers by Hopsoft](https://github.com/hopsoft/stimulus_controllers/tree/master/controllers/src) features a collection of useful Stimulus controllers like auto-suggest and copy to clipboard.

[Stimulus Form Utilities by Hopsoft](https://github.com/eelcoj/stimulus-form-utilities) is a collection of useful form helpers like characters count for any input field and auto text-field resizing.

[StimulusReflexGlobalId](https://github.com/joshleblanc/stimulus_reflex_globalid) automatically maps global IDs to instance variables during a reflex.

[StimulusShortcut](https://github.com/leastbad/stimulus-shortcut) for simple binding of keystrokes to element actions.

## Community

[Community site for StimulusJS](https://discourse.stimulusjs.org/)

## Related Projects

[Motion](https://github.com/unabridged/motion) is an integrated framework for reactive, real-time frontend UI components in your Rails application using pure Ruby that is probably the closest direct alternative to StimulusReflex.


[Matestack](https://www.matestack.io/) is another alternative 


[Hyperstack](https://hyperstack.org/) is a Ruby DSL, compiled by Opal, bundled by Webpack, powered by React.

Build modern, reactive, real-time apps with Django in Python with [Sockpuppet](https://github.com/jonathan-s/django-sockpuppet)

[Reactive Laravel](https://github.com/livewire/livewire)

[Reactive Phoenix](https://github.com/phoenixframework/phoenix_live_view) is written in Elixir and inspired this whole thing.

[Reactive ASP.NET](https://github.com/dotnet/aspnetcore/blob/master/src/Components/README.md)

[Prism](https://github.com/prism-rb/prism) is a framework for making web applications with Ruby and WebAssembly

## Credits

_Hat tip to [Skatkov](https://github.com/skatkov/awesome-stimulusjs) for the idea._
