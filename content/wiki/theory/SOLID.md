---
title: SOLID
menu:
    wiki:
        parent: principles
description: Description of the 5 principles and practices that make up the SOLID acronym
---

S.O.L.I.D.
==========

S.O.L.I.D. aka SOLID stands for:

S: Single Responsibility Principle aka SRP
------------------------------------------

A class should have a single responsibility.

O: Open / Closed
----------------

A class should be open for extension, but closed to modification.

L: Liskov substitution principle
--------------------------------

An object should be replaceable with an object of its subtype without breaking the program.

I: Interface Segregation Principle
----------------------------------

Many interfaces are desirable over one general-purpose interface

D: Dependency Injection Principle aka DI
----------------------------------------

Classes should depend on supplied abstractions, instead of concrete implementations.

This is usually extrapolated into these abstractions being supplied by a container, so that consumer objects are
not responsible for instantiating and configuring its dependencies.
