+++
title = "Call for early adopters of Sel, Botan and one-time-password"
description = ""
date = 2024-04-05T16:00:00
updated = 2024-04-03T16:00:00
draft = false
template = "blog/page.html"

[extra]
lead = "We are calling for early adopters of libraries under the stewardship of the Haskell Cryptography Group."
+++

The Haskell Cryptography Group is calling for early adopters of [sel], [botan-low], and [one-time-password]
which provide reliable and well-documented bindings to [libsodium][libsodium] and [botan], as well as an implementation of OTP codes (TOTP and HOTP)
backed in large part by `sel`.

We want to gather feedback from industrial and hobbyist users on the documentation and ergonomics of these libraries,
as this will help us serve users better in the future.

In particular, we want to know if the example usages provided in the documentation help, and how they could be improved.

You can use these libraries today by adding them to your cabal file:

```haskell
sel ^>=0.0.1,
```

```haskell
one-time-password ^>=3.0.0,
```

and
```haskell
botan-low ^>=0.0.1,
```


For security reasons, the bindings do not bundle the underlying C and C++ libraries, you have to install them yourself:

* [Botan3 building from source](https://botan.randombit.net/handbook/building.html)
* [Libsodium in package repositories](https://repology.org/project/libsodium/versions)

Please let us know if you have any issue on the the ticket trackers:

* [Libsodium bindings tracker](https://github.com/haskell-cryptography/libsodium-bindings/issues/new)
* [Botan bindings tracker](https://github.com/haskell-cryptography/botan/issues/new)
* [one-time-password tracker](https://github.com/haskell-cryptography/one-time-password/issues/new)


[sel]: https://flora.pm/packages/@hackage/sel
[botan-low]: https://flora.pm/packages/@hackage/botan-low
[one-time-password]: https://flora.pm/packages/@hackage/one-time-password
[libsodium]: https://doc.libsodium.org/
[botan]: https://botan.randombit.net/
