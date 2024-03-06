+++
title = "Botan: The first milestone"
description = "A step towards improving the state of Haskell cryptography"
date = 2024-06-03T12:15:00
updated = 2024-06-03T12:15:00
draft = false # Leave this as true so that it is not published
template = "blog/page.html"

[extra]
lead = "After 8 months of work, we've reached an important milestone. Now we're here to tell you about what is coming next."
+++

# Botan: The First Milestone

First off, huge thanks to [Mercury][mercury] for funding the [first proposal][first proposal] and helping us reach this milestone - this library would not be in this state without their support. If you are an engineer looking for a savvy place to work, I hear they are [hiring][mercury hiring]!

With [botan-bindings][botan-bindings] and [botan-low][botan-low] having reached their initial `0.0.1` release and `botan` making it to [package candidate][botan] status, we've reached an important milestone - the first released version!

After 8 months of work, celebrations were in order, and after a bit of a breather, we're back in action to tell you about what is coming next.

But first...

# A call for users

Do you use one of the following libraries?

- `crypton` / `cryptonite`
- `libsodium`
- `saltine`

What are you using cryptography for? Would you be interested in trying something new? Perhaps an alternate backend for your cryptography needs?

We're working on `botan`, a cryptographic kitchen sink, and could use your feedback! We've successfully published `botan-bindings` and `botan-low`, and now are hard at work on getting `botan` ready too. That's where you come in! We can't listen to your feedback if there isn't any.

`botan-low` is surprisingly viable out-of-box, and `botan` will be having it's own `0.0.1` release soon enough. We are interested in seeing how they perform in the real world, and we can only do that with users!

Or perhaps you may be a user of a library with one of these buried deep in the dependencies?

- `amazonka-core`
- `hpack`
- `scotty`
- `servant`
- `stack`
- `tls`
- `x509`
- `warp`
- `websockets`

There's some pretty popular libraries on that list there, and their list of transitive dependents is quite large. These libraries sit at the root of a lot of production haskell code, and anything involving networking, APIs, and the internet is likely to depend on at least one of them. 

Would it surprise you that they are all directly or indirectly dependent on `crypton`, which contains unaudited C implementations that must be maintained by the Haskell community as a fork after `cryptonite` was abandoned by its original author.

This is a problem, and we're trying to change that with bindings to `botan`.

Having a solid, reliable, and well-maintained cryptography libraries is a huge benefit to the Haskell ecosystem in general, and is essential for most commercial and industrial use cases.

What are you using cryptography for? Let us know in the comments or with upvotes.

# Who are we?

I am Leo Dillinger, a member of [Haskell Cryptography Group][haskell cryptography group], and I am working with the [Haskell Foundation][haskell foundation] to develop free and open-source software for you and the Haskell ecosystem.

# What are our goals?

We seek to provide trusted, open-source cryptography solutions to you. Much of the existing Haskell cryptography ecosystem is aging, unmaintained and unaudited, or very limited in scope, we are seeking to improve that.

# What is Botan?

Botan is an comprehensive, open-source, BSD-licenced, C++ cryptography library with a stable C API. It offers a broad variety of functionality and algorithms, including **post-quantum cryptography**, is developed and maintained by an active community, and has been [audited][botan audit] in the past.

By binding to Botan, we have solved a significant problem of providing much of the necessary 'cryptographic kitchen sink' via a suitably performant, suitably licensed, open-source library. Furthermore, we do this without imposing a large maintenance burden on the Haskell community, as we are not required to maintain the Botan cryptography library itself, only the bindings to it.

See the
[first proposal][first proposal] for more details.

# A new phase

As we all know, perfect is the enemy of good; no software is perfect the first time, and we release things when they work, and then continue to improve them. And so we hope that this is simply the first version and first step on a journey of many improvements small and large.

With this milestone, the project enters a new phase in the software development lifecycle - maintenance and development. During initial development, we were nimble, and could make choices arbitrarily - but now that we have something that works, with an initial release and users, we have to keep it working all the while we continue further development. We now have other people invested in this, and can't make choices willy-nilly - we owe it to our users and stakeholders to listen to them.

# The second milestone

That is what this next milestone is about - listening to feedback, improving the user experience, and seeing where the pain points are. Here's what we've heard, and here's what we're planning for the next three months.

## Improved installation support

One of the biggest pieces of feedback that we've received is the need for improved support for the installation of the `botan3` C++ library. This was a recurring item, and we've heard you loud and clear.

We'd like to spend a good chunk of time improving the installation process, with a specific focus on Windows[^1] and Linux support, working on the CI + unit tests for improved reliability and reporting overall.

[^1]: Definitely more highly requested than anticipated

We're also looking into using `build-type: Configure` for bundling Botan C++ as a Haskell package for easy installation on all operating systems - we'd like for usage to be as easy as adding `botan` to your dependencies.

## Development of a drop-in interface replacement for `crypton`

This is obviously on our mind, given our call for users, and was mentioned several times in feedback. `crypton` is a dependency in many important libraries in the Haskell ecosystem, and we would like to build an interface that is as near a drop-in replacement for `crypton` as possible.

There will be some differences, as `botan` doesn't necessarily support everything[^2] in the same way as `crypton` does, but we'll give it our best effort to make migration as simple as possible.

[^2]: There are a few things that `crypton` supports that `botan` doesn't, but also vice versa - `botan` supports things like modern post-quantum algorithms and `crypton` doesn't.

## Development of a high-level libsodium-like interface

We'd like to expose a high-level libsodium-like interface of selected best-in-class algorithms in order to make usage dead simple. We don't want you managing primitives yourselves - we want you calling a simple function purely or in an appropriate monad / transformer.

> This might be a bit of a stretch goal, in favor of focusing on replacing `crypton`.

## Continued development of the cryptographic typeclasses

The development of [cryptographic typeclasses][cryptographic typeclasses] is ongoing, in an effort to improve per-algorithm type safety and ergonomics through more consistent handling of cryptographic primitives such as keys, nonces, and ciphertexts.

> This is also a necessity for the `crypton` drop-in replacement.

## Continued refinement of `botan`

There are many continued refinements and improvements to the `botan` library that we would like to apply. 

Improved error handling is a big one, as we'd like to use `HasCallstack` appropriately throughout the library.

We'd also like to work on the `MonadRandomIO / NonDeterministic` monad in order to integrate with `random` and take advantage of the `Uniform` class to make sampling / generation of random data easy.

We'd like to also take advantage of the secure memory erasure by providing functions for creating temporary objects that are automatically zeroed when they go out of scope. This is a big one, we don't want sensitive data hanging around in memory.

Finally, we'd also like to continue improving, unifying, and standardizing the `botan-low` bindings for consistency overall, as the techniques for binding to functions were refined over time, and have not been evenly applied.

---

These are some of the things that we'd like to accomplish over the coming months.

You can find more details in the update[^3] [second funding proposal][second proposal]. This proposal is a continuation of the efforts of the first proposal, and is motivated by the same long-term goals.

[^3]: Update is not yet live at time of writing - if it hasn't been updated yet at time of reading, check back in a day or so.

# A flag planted on the horizon

As part of the Haskell Cryptography Group, we're about more than just maintenance of existing libraries - we want to develop a full suite of modern cryptography libraries.

Cryptography is a different niche, but we see the success of Haskell web server libraries as an example of a healthy, community-driven ecosystem. There are packages ranging from the low-level like `wai` supporting multiple backends from the swiftly simple `scotty` to the deeply complex `servant`, frontends like `blaze-html` and `lucid` - a rich set of libraries that provide a flexible enough set of solutions at whatever level of abstraction you need, that take full advantage of Haskell's powerful type system.

We see the success of the haskell web server ecosystem as an example of a healthy, developed niche, and as an example of Haskell making something safer and easier to use - something that we aspire to do with cryptography.

That level of development takes work, and time, and we've just hit our first milestone - bindings to a modern, stable, audited open-source cryptography library. Now begins the long work of establishing an ecosystem on top of it.

Here's what we're looking into for the long-term future:

## Improving APIs with higher-order functions

We'd like to build higher-order functions to take care of complicated server/client multi-step algorithms, such as SRP6. Bundling up the necessary sequences of actions into a higher-order function that takes a couple of IO functions as arguments is a safer, more ergonomic, and more reliable way of performing these actions than handing the user a series of steps that they must call in the right order.

## Integration into libraries as an alternative to `crypton`

We'd like to integrate `botan` with other libraries as an alternative to or replacement for`crypton`, either through the drop-in interface, or by migrating entirely - and we'd like to make that easy by providing the appropriate tools and flags.

Of particular interest is the Haskell web ecosystem, which currently relies heavily on `crypton`.

## Split off cryptographic classes as a separate package to be backend agnostic

We see `botan` as one of many potential backends, and backend-agnostic cryptographic typeclasses are like `wai` - a common interface. There is a difference between algorithms (sets of operations) and typeclasses (specific use cases). Algorithms are 'how we do it', typeclasses are 'what we want to use it for'. If we've defined our typeclasses correctly (as by use case), they should be backend-agnostic, regardless of the particulars of the implementation - otherwise the implementation could not fulfill its duties.

For the moment, these classes are part of `botan`, and we'd eventually like to split these cryptographic classes off into their own `cryptography` library.

## Implementation of more advanced algorithms

There's a whole host of interesting and useful cryptography algorithms that have been developed in the last decade - including post-quantum cryptography, and we'd like to be able to provide them as tools for you to use.

Once we have a stable foundation, such as `botan`, we want to move on to implementation of more advanced algorithms, such as Merkle trees and Signal's [Double ratchet][double ratchet] / [Apple's PQ3][apple pq3]

We don't want you to be messing around with cryptographic primitives - we want you importing libraries like `double-ratchet`[^4] and `sparse-merkle`[^4] and `distributed-json`[^4] instead of having to implement it yourself.

[^4]: These libraries do not yet exist, but we'd like them to.

## Building an application framework that takes care of cryptography & security

Ultimately, we'd like to build an application framework that abstracts away cryptography & security, not unlike how the Haskell web ecosystem successfully manages away much of the complexity of HTTP servers. We'd like to develop a comparable system, but for cryptography - one that comes with modern post-quantum key exchange and encryption and secure transport built-in. Wouldn't that be something - an application framework with out-of-box working post-quantum transport scheme?

Easy-to-create applications with built-in security could be a killer application for Haskell, in an era where data safety is becoming a primary concern.

# How can you help?

We've already taken the first step of binding to a modern, stable cryptography library. Now it is time to take the next. We'd like to ensure the longevity of this project as we tackle the next set of challenges.

We need users, and we need sponsors!

You can help us by commenting, voting, or pledging support - your activity here lets us know that you are interested in what we've done and what we're going to be doing. but it also has a tangible effect of demonstrating the ongoing success of this project!

Help us keep going! Follow the [devlog][devlog] for more frequently updated details!

# Signed

Leo Dillinger,  
Haskell Cryptography Group

Hecaté,  
Haskell Cryptography Group

Jose Calderon,  
Executive Director, Haskell Foundation

### Appendix: Links

[haskell cryptography croup]: https://haskell-cryptography.org/ "Haskell Cryptography Group"

[haskell foundation]: https://haskell.foundation/ "Haskell Foundation"

[mercury]: https://mercury.com "Mercury"

[mercury hiring]: https://www.reddit.com/r/haskell/comments/1akeujj/comment/kp7g0rf/ "Mercury hiring"

[botan-bindings]: https://hackage.haskell.org/package/botan-bindings-0.0.1.0 "botan-bindings"

[botan-low]: https://hackage.haskell.org/package/botan-low-0.0.1.0 "botan-low"

[botan]: https://hackage.haskell.org/package/botan-0.0.1.0/candidate "botan"

[botan audit]: https://botan.randombit.net/releases/audit_1.11.18.pdf "Botan audit"

[first proposal]: https://github.com/haskellfoundation/tech-proposals/pull/57 "First proposal"

[second proposal]: https://github.com/haskellfoundation/tech-proposals/pull/64 "Second proposal"

[devlog]: https://discourse.haskell.org/t/botan-bindings-devlog/6855/ "Devlog"

[cryptographic typeclasses]: https://discourse.haskell.org/t/botan-bindings-devlog/6855/ "Cryptographic typeclasses"

[double ratchet]: https://signal.org/docs/specifications/doubleratchet/ "Double-ratchet"

[apple pq3]: https://security.apple.com/blog/imessage-pq3/ "Apple PQ3"


