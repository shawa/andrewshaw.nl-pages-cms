---
title: "Reviving Genius"
subtitle: "Getting a 17 year old app to build on macOS again"
category: code
date: 2025-07-07
tags: [objective-c, macOS]
---

> **EDIT**: I've had some feedback from [HN readers](https://news.ycombinator.com/item?id=44540724), and I've learned some interesting things since writing this post!
>
> For one, after this whole journey I thought that _surely_ it is easy enough to type in answers on Anki, and indeed it is. In the card's template, you can add an entry `{type:FieldName}` to the front, where you are asked to type in whatever `FieldName` is. So in my "Frequency Dictionary of Dutch" deck, I've added `type:Definition`.
>
> Secondly, I actually [read the manual for Anki](https://docs.ankiweb.net/deck-options.html#learning-steps), and they have a great explanation of what the _Again / Hard / Good / Easy_ buttons actually _do_ to the underlying repetition model. What I liked about Genius was how straightforward it was to understand _why_ you're seeing or not something during a review session.
>
> Finally the post had some typos, and a couple of errors. Thanks to `aaronbrethorst` for pointing out that `+` and `-` are for instance, and class methods, not public/private.

In my recent foray into learning Dutch for my relocation to the Netherlands -- I'm sure there'll be much to blog about -- I fell victim to the siren song of the Green Owl again.

It's too tempting - you get showered with instant feedback, encouragement in-app rewards, social stuff etc. To be fair it is fun, and you really feel that you're doing something useful.

...except.

I last used it in earnest it to 'learn' German before a trip to Berlin. I racked up a 150+ day streak or something nuts like that, a good 15 mins per day which they deem pretty high, and then turned up utterly unable to speak or read anything of actual utility

> die Frau ist kein Klavier
>
> am Dienstag spreche ich nicht mit dem Apfel

Now I don't think it was always like this, and really it's for another blog post to enumerate the all of the ways it's been enshittified but suffice to say it's just not for me anymore.

## Flashcards and Anki

On the other end of this gamification spectrum is just hard flashcards. Learn the thing on the other side of this card. Your reward is the number of stuff you've learned, and if you 'break your streak', that's on you - you're just not learning anything.

Now, people swear by Anki.

I've friends who've learned all the world flags, taught themselves to recognise basically any painter by their style etc. Really cool stuff. I think though, for whatever way I ingest language and information, it's not so good for me.

Specifically I think I'm missing clear right/wrong feedback (rather than judging if I was 'good' or 'bad' at remembering it), as well as the mechanics of actually having to type out the answer.

In school and university I found that unless I was actually taking notes, and actually writing text, or even typing, I was just _not_ engaging enough.

And so, when flipping over Anki cards and saying them in my head, it just sort of feels like temporarily stimulation of short-term memory.

Despite the spaced repetition, nothing seems to go in, and so I've just not been able to build a good habit with it.

(I think there are cards where you have to type the answer in, but truth be told I haven't really dug into that)

Now though this brings me to my holy grail, white whale app, from **years** gone by.

## Genius

Genius was a spaced repetition app originally written by [John R Chang](https://jrcpl.us/) for his own needs. It uses a comparatively simple (to Anki) but still very effective spaced repetition app for learning flashcard-like associations.

And, it was _so simple_. You have 2 columns to enter the things you want to learn (the cue), and you're quizzed on them (the answer).

Plus, it had _just_ the right amount of instant-gratification, reward conditioning sounds in the form of the OS X _Basso_, _Blow_, _Funk_.

<img src="https://a.fsdn.com/con/app/proj/genius/screenshots/152532.jpg/max/max/1" width="600">

Alas, development stopped sometime around 2008, and despite an impressive run, it no longer runs on macOS:

```txt
/Volumes/Genius/Genius.app/Contents/MacOS
> file Genius
Genius: Mach-O universal binary with 2 architectures: [ppc:
- Mach-O executable ppc] [i386:
- Mach-O executable i386]
Genius (for architecture ppc):  Mach-O executable ppc
Genius (for architecture i386): Mach-O executable i386
```

Yes, PowerPC, and i386 (32 bit) only. We're a few architectures past that!

## Reviving Old Software

As an aside, I've been really impressed by some recent really cool software/tech conservation, people are doing.

See stuff like [MattKC and co's Lego Island decompilation](https://www.youtube.com/watch?v=gthm-0Av93Q) where they have reverse-engineered and entirely reimplemented whole swathes of the game. Or the [Frogger source code recovery](https://github.com/Kneesnap/onstream-data-recovery/blob/main/info/INTRO.MD)

Or on the hardware side, [the saving of the world's largest CRT TV from a closing-down soba restaurant in Osaka](https://www.youtube.com/watch?v=JfZxOuc9Qwk) (this is seriously a good watch).

Anyway I figured, if feckin _Lego Island_ can be decompiled, and people can save code from ancient proprietary magnetic tapes, surely it's not beyond the wit of man, me, to get Genius to work again.

<img src="/assets/images/blog/07/genius-needs-to-be-updated.png" width="300" />

_Maybe I can be that developer :)_

## Source Code

The homepage is <https://genius.sourceforge.net>. With some clicking about, you'll find the link to the [source code](https://sourceforge.net/p/genius/code/HEAD/tree/), an SVN repo. I'd only ever heard of SVN from my elders in university - something about locking, a 'check out' being an actual 'check out' as one acquires an exclusive lock on a library book.

I'm not interested in plumbing those depths, but luckily [`git-svn`](https://git-scm.com/docs/git-svn) is.

So after much waiting, I ended up with a neat git repo. It's jarring to pop open a familiar git log and see commits from _2004_:

```txt
commit 5d5624365ab06b08bb83257e78d1bc44bbca7664
Author: jrc <jrc@f73e0bdd-8638-0410-8bb3-c52e70a1423d>
Date:   Sat Nov 6 02:29:42 2004 +0000

    loc 1

commit a2045bf7f2d5ed93f73893edce72665ea260453e
Author: jrc <jrc@f73e0bdd-8638-0410-8bb3-c52e70a1423d>
Date:   Sat Nov 6 02:28:42 2004 +0000

    *** empty log message ***

commit 1d9e71e3fafe91d182a244b3bf5fc1173348dfcb
Author: jrc <jrc@f73e0bdd-8638-0410-8bb3-c52e70a1423d>
Date:   Tue Oct 19 21:53:33 2004 +0000

    This commit was generated by cvs2svn to compensate for changes in r2,
    which included commits to RCS files with non-trunk default branches.

commit 62485d30ab237f05d04e2791a9e6871b9adbf701
Author: (no author) <(no author)@f73e0bdd-8638-0410-8bb3-c52e70a1423d>
Date:   Tue Oct 19 21:53:33 2004 +0000

    New repository initialized by cvs2svn.
```

I love how everything repeats itself. I wonder what was in the CVS source.

## Building for macOS

As it turns out, it was surprisingly easy to get the project to build!

The `.xcodeproj` format still seems to be entirely forwards-compatible, and it opened up completely fine on the latest developer tools, on my arm64 macbook.

Building failed, as it was unable to locate the old OS X 10.4 SDK it was hard-coded to require.

But changing this to the latest tooling let the obj-c compiler actually run, with a compiler error!

```objective-c
GeniusAssociationEnumerator.m:265:87 Incompatible function pointer types sending 
  'int (id, id, void *)' to parameter of type 
  'NSInteger (* _Nonnull)(id _Nonnull, id _Nonnull, void * _Nullable)' 
    (aka 'long (*)(id _Nonnull, id _Nonnull, void * _Nullable)')
```

Looks like type checking got a little bit more strict.

A _single line change_ fixed the build:

```diff
//! randomly returns NSOrderedAscending or NSOrderedDescending
-int RandomSortFunction(id object1, id object2, void * context)
+NSComparisonResult RandomSortFunction(id object1, id object2, void * context)
 {
     BOOL x = random() & 0x1;
     return (x ? NSOrderedAscending : NSOrderedDescending);
```

[`GeniusAssociationEnumerator.m`](https://github.com/shawa/genius/commit/39f26bed7e5bde146bd05aadacbe33e2d2432386#diff-dd1391d7c026c37eb147d2c8adace5dbd76bbfb738780d502584f51b9f6c281eR16-L37)

_As an aside, surely it's really confusing as an Objective-C developer reading diffs when it uses `+` and `-` to denote class/instance methods?_

...and it **ACTUALLY BUILT**.

<img src="/assets/images/blog/07/broken.png" alt="Broken Genius build screenshot" width="600" />

It looks a bit janky, but it works!

The next hurdle was getting Xcode to read the old `nib` files for the UI. I've admittedly little idea how it works, but they seem so old that even Xcode can't convert them. Fortunately there is `ibtool`, which has an `--upgrade` option to replace them.

After a little bit of messing about in Interface Builder, upscaling the icons, and fixing some text clipping, we get a fairly snazzy, modern looking macOS app! And it's completely functional, fully compatible with the original `.genius` card decks I created years ago.

<img src="/assets/images/blog/07/working.png" alt="It works! Learning Dutch vocab" width="600" />

Projects like this are certainly fun, and valuable in their own right. I've learned a relative ton (compared to my zero knowledge) about mac development, took a nice trip down memory lane with the different architectures, etc.

However ultimately Genius was written to aid memorisation, and now I'm happily using it to do just that, just as I did back in 2008!

<img src="/assets/images/blog/07/quiz.png" alt="Genius Quiz" width="600" />

<img src="/assets/images/blog/07/festeta.gif" />

You can browse the updated source code at <https://github.com/shawa/genius>.
