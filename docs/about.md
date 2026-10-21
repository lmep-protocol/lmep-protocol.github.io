# Welcome to LMEP

## Purpose

LMEP (Lightweight Message Exchange Protocol) is an instant messaging protocol for
persistent community messaging between users over a network.

LMEP is language-agnostic, meaning that it can be implemented by clients and
servers written in different programming languages

## Terminology

`Chathome`
> A collection of related chatrooms managed by one or more admins

`Homeowner`
> The manager/admin of a chathome

`Chatroom`
> A logical channel within a home where messages may be exchanged

## Scope

This specification defines:

- The LMEP client-server architecture
- Connection and transport requirements
- Message framing
- Command syntax and server responses
- Structure of chatrooms
- Optional features

## FAQ

### Why another Instant Messaging Protocol?

Because nothing out there sat right with me. The closest I could find were IRC
and XMPP, but they have a few major flaws or design philosophies I disagree with.

### Why not IRC?

IRC was originally created back in 1988 and is a tried and trusted protocol by many.
In fact, I created this protocol to act, not as a drop-in replacement to IRC, but
to serve as an alternative to it. IRC has some issues which make it unusable to
me, such as:

- IRC has no unique user identifications, and relies solely on nicknames to identify users, which can lead to nickname collisions
- There is a lack of modern features on IRC, such as replies, pinned messages, message histories and whatnot.
- Presence information is very limited. It is not formalised within IRC and only tracks basic user statuses and availability
- Encryption can be difficult to configure on the IRC client. Many channels allow you to connect over plaintext

### Why not XMPP?

XMPP is an excellent protocol that solves many of the shortcomings of IRC. However,
it has two major design decisions that I really don't agree with:

- Messages and other data sent over XMPP are structured as XML elements. LMEP is designed not to rely on XML because it creates major server overhead and uses up a lot of bandwidth
- XMPP is a general-purpose messaging protocol whose community messaging functionality is provided through MUC and other extensions. LMEP is purpose-built around persistent community messaging.
