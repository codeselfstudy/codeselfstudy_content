---
title: How to Install Erlang's egd Library in Elixir
date: 2017-09-02
path: "/blog/how-to-install-erlangs-egd-library-in-elixir/"
---

I needed to use <a href="https://github.com/erlang/egd">Erlang's egd library</a> on Ubuntu 16.04, but was having a difficult time figuring out how to do that. After some searching, I finally found the answer:


To install egd in an Elixir project, just add this to your dependencies and run <code>mix deps.get</code>:

```elixir
{:egd, github: "erlang/egd"}
```
