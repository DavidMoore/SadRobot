---
title: Covariance & Contravariance
parent: "net"
menu:
    wiki:
        parent: "net"
---

* Covariant if it preserves the ordering of types (≤), which orders types from more specific to more generic;
* Contravariant if it reverses this ordering;
* Bivariant if both of these apply (i.e., both `I<A>` ≤ `I<B>` and `I<B>` ≤ `I<A>` at the same time);
* Invariant or Nonvariant if neither of these applies.

In C# interfaces, `in` represents contravariance, and `out` represents covariance.

For example in C#, if `Cat` is a subtype of `Animal`, then:

`IEnumerable<Cat>` is a subtype of `IEnumerable<Animal>`. The subtyping is preserved because `IEnumerable<T>` is covariant on `T`.

`Action<Animal>` is a subtype of `Action<Cat>`. The subtyping is reversed because `Action<T>` is contravariant on `T`.

Neither `IList<Cat>` nor `IList<Animal>` is a subtype of the other, because `IList<T>` is invariant on `T`.

https://en.wikipedia.org/wiki/Covariance_and_contravariance_(computer_science)
