# Work in Progress, public release on January 21th (Wordle-prick-day)

# mordle.github.io

Best interview with Josh "Wordle" Wardle: https://slate.com/culture/2022/01/wordle-game-creator-wardle-twitter-scores-strategy-stats.html

Multiplayer: https://www.youtube.com/watch?v=uvCl39bemp0

2.2MB Welsh version: https://www.hiriaith.cymru/gairglo

And before you send me hate mail; here is the copyright:

![](https://i.imgur.com/b96worl.png)

I had heard of Wordle before, but I opened the site only after I heard it was created with Web Components technology.

So after guessing the word of the day, I hit F12 and dove into the source code.

Nothing unfamiliar to me, I have this "hackers" attitude since I first pressed the ESC key on a TRS-80 keyboard to change my high-scores. You can't blame me, I was 10.

Josh has done a decent job. He uses a hash to name his _one and only_ JavaScript file, so you can't easily link to it, and hijack his code.

I then ran my (personal) Qomponent Inspector on the code. This does a _dive_ into the DOM, and lists (the first used) copy of all used Web Components.

As you can see below, there isn't much Web Components going on. They are mainly used only to render content. The meat and bones of Wordle is in the `<game-app>` Web Component.

And it did not take long to spot a very interesting property! **gorge** was todays correct word!

![](https://i.imgur.com/h8ivuGz.png)

## Diving deeper, into the rabbit hole

I then dove deeper into the JavaScript source code, and quickly spotted **all** words are readable in the source code. Being a single JavaScript file, it is very easy to copy and **_change_** the original source code, and create your own (localized) version.

Too easy... I did that type of changes on BASIC sources way back in 1979 on that TRS-80

I could have rewritten the app with (slightly) better use of Web Components. But I wanted to keep the code as simple as possible, and I wanted to keep it as close to the original as possible.

Why, you ask? Because I wanted to make it as easy as possible to create **YOUR OWN** version of Wordle.

**Using Josh his original code!**

**100% of his original code!**

And when I learned "danny" is a valid Wordle word. I decided to see how far I could get.

REMEMBER! I am absolultely **NOT** making ANY changes to Josh his code!

# Web Components are Web Components are Web Components

The whole fun of native Web Components is reusability and extensibility. That means you can use the **ORIGINAL** source code and **EXTEND** on it.

1 picture says more than 2 words:

![](https://i.imgur.com/Taw5g55.png)

You DO need knowledge about HOW Web Components **function**. That is why I built my Qomponent Inspector.

But, still, I had challenges challenges. Josh did not provide documentation, and his source code is minified.

## Your own Wordle solution word

Using Chromium Browser **sources/snippets** you need only a few lines of code to create you own ``<my-game>`` Web Components, which **extends** from Josh his original ``<game-app>`` Web Component.

![](https://i.imgur.com/Vhm0AVH.png)

```

```

## Wordled JSFiddle

In a JSFiddle you copy all of Josh his JavaScript (from one file) in the JavaSscript section.
Also copy the ``<STYLE>`` tag **content** from his ``index.html`` file to the JSFiddle CSS section.

{% jsfiddle https://jsfiddle.net/WebComponents/x8eyv1f4 %}

### Lessons learned:

- Web Components can be **extended** from **existing** Web Components. Most of us call this using a **BaseClass**

- Web Components can be created **after** definition in the DOM, all instances will automagically **upgrade**

But why stop there? I am not a 10 year old _scriptkiddie_ hacking away in BASIC anymore.

Let's up the ante


# [more on friday]


### You can't overload Wordles Web Components

``customElements.define("game-toast", class extends HTMLElement{});``

Because Josh his code does not do any error checking for existing Component names. The App will just blow up.

![](https://i.imgur.com/xf6plEx.png)


## attributeChangedCallback

This callback **before** the connectedCallback, when there are **observedAttributes** on the Custom Element.

So you have to safeguard against premature eja.. eh.. execution with

```
if(oldValue){
    ... your code
}
```

This is something most Tools shield you from. But remember: _a Fool with a Tool is still a Fool_.
Learn the Technology first, then find yourself a Tool that does the job better!

# Wordle blogs on the web

- https://dev.to/akaak/wordle-guess-the-hidden-word-in-6-tries-2i4c
- https://world.hey.com/johnt/reverse-engineering-wordle-4d06a6a1
- https://24htech.asia/when-will-wordle-end-heres-how-long-you-can-play-the-viral-game-s469296.html

# Wordle on the web

- Dutch version https://woordle.nl/ (62 kB, created with Elm)
- React versions

  - https://octokatherine.github.io/word-master/ (126 kB)
  - https://61dc4dbf9f2b9d0007925c02--thirsty-hoover-08af60.netlify.app/ (71 kB incomplete UI/UX)

- Funny alternatives:
  - https://www.theverge.com/tldr/2022/1/11/22877996/wordle-spoofs-alternatives-letterle-sweardle-queerdle


# Learning Web Components

Just play! play! play! You only learn this by doing.

And don't grab a tool and think you are done. 

Learn the technology first, then find yourself a tool that does the job better!

_A Fool with a Tool, is still a Fool_

But don't take this from me, I am just an old geezer who in 1979 hit the ESC key on a TRS-80, and learned to program.

![](http://www.trs-80.org/img/salesunits.png)

