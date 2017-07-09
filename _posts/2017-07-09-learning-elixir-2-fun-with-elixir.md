---
layout: post
title: 'Learning Elixir #2: Fun with Elixir'
date: 09 Jul 2017
categories: analysis
author_name: Mike
author_url: /author/mike
author_avatar: mike
show_avatar: false
read_time: 2
feature_image: feature-work
show_related_posts: true
square_related: feature-work
location: Providence
---

In [this video about the actor model](https://channel9.msdn.com/Shows/Going+Deep/Hewitt-Meijer-and-Szyperski-The-Actor-Model-everything-you-wanted-to-know-but-were-afraid-to-ask) (which I shared in my [last post]({% post_url 2017-07-06-learning-elixir-1 %})) Hewitt talks about indeterminacy. Indeterminacy goes hand in hand with robust concurrency. He spoke of an actor, who upon receiving a start command will send two messages, a "go" message, and a "stop" message. They are sent via the _ether_, that is: they leave any formal, theoretical channel of the programming language and route via the real world of hardware. Consequently, there's no guarantee which one will arrive first.

* If the "go" message is received, a counter is incremented, and another "go" message is sent.
* If the "stop" message is received, we report the counter and exit

The result is an arbitrarily large count.

Of course I want to test this out for myself. In day four of the elixir intro from DailyDrip, [Processes and Messaging](https://www.dailydrip.com/topics/elixir/drips/processes-and-messaging-08687de7-07c6-4cc3-b6c6-4398d137820c), the example code creates an actor that an send "ping" and "pong" messages back and forth. This is the first concrete elixir code I've seen that uses messages. I'll use that example to try to model Hewitt's indeterminacy example.

After a bit of kludging, I ended up with this:

```elixir
defmodule Indeterminacy do
  def start do
    loop()
    # send(proc, {:go, 0}) #run this in iex
    # send(proc, {:stop}) #run this in iex, too
  end

  def loop do
    # receive pattern matches on a series of potential messages and runs 
    # some code when it receives that message. Here we're handling 
    # "stop" and "go" messages
    receive do
      {:stop} -> 
        IO.puts "We've been asked to stop"
        Process.exit(self(), "I don't know a better way to terminate yet")
      {:go, counter} -> 
        IO.puts "go #{counter}"
        send(self(), {:go, counter + 1})
    end
    loop()
  end
end
```

Right away, I ran into some trouble figuring out how to display the count on receiving the "stop" message, as I'm not sure how an actor manages shared state. I didn't want to use my time for that, so I simply printed the counter on receipt of the "go" message.

This code seems to work fairly well, but after `iex -S mix` in the working directory, I ended up with appears to be a single threaded repl, and don't know how to actually send two messages simultaneously. Instead, the results depend entirely on which of the two messages I send first, or how quickly I managed to send "stop" following "go".

Executing this:

```
proc = spawn(Indeterminacy, :start, [])
send(proc, {:go, 0})
send(proc, {:stop})
```

...from a script wasn't any more interesting:
 
```
go 0
We've been asked to stop
```

I'm definitely missing something here! Perhaps my system needs a more turbulent ether. Perhaps it's that I'm not sending these messages simultaneously. I could try adding sleeps at some point in the execution, but that would hardly be a test to demonstrate inherent indeterminacy.

In any case, this was fun, and I'll resume my daily drip lessons tomorrow. I've enjoyed this self-guided tour, despite not finding precisely what I'd set out to!