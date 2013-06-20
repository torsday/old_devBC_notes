# Networking, Streaming and Messaging

The goal of the encoding lecture was to introduce you to the skill of _recognizing structure in encoded data_.

Given this sequence of characters:

    { "name": "Myles Byrne", "city": "SF" }

Any developer who's opened a text editor can say "JSON!" or "A user object!" but it takes deliberate and precise cognitive work to say:

> A mapping of keys to values.
> There are two elements in this mapping.
> In both cases the key is a string and the value is also a string.
> Semantically it appears to be information about a person.
> Syntactically the encoding looks like JSON.

We do two main things with encoded structured data:

1. Send and receive it from other programs
2. Store it somewhere for retreival later

Note that #2 can be done with #1. You can write a program that runs on a computer with little memory and no disk as long as you can make some other program on the network responsible for storing things and then retreiving them some time in the future.

Just like with structured data, when you show a beginner programmer two programs communicating with each other over some channel they'll immediately focus on the encoding - "oh look, it's *just* JSON!".

(While the word "simple" still holds the title for the most misused word by programmers, the word "just" is a close second)

If you ask them to zoom out they'll likely go to far in the other direction: "it's a TCP socket!", "it's a WebSocket!", "it's Redis!"

The goal of today's lecture is to introduce you to the skill of _recognizing patterns in program communication_. 

These patterns sit above the transports (TCP, Pipes, WebSockets) and below the encodings (JSON, HTTP, Google Protocol Buffers) and are crucial to understanding how multiple programs running on different machines (or even different prcesses on the same machine) can work together to peform a single task such as rendering your facebook profile page.

***

Message pattern resources

* https://github.com/visionmedia/axon
* http://zguide.zeromq.org/page:all

Transport/Channel resources

* http://en.wikipedia.org/wiki/Network_socket
* http://en.wikipedia.org/wiki/Pipeline_(Unix)
* http://en.wikipedia.org/wiki/Berkeley_sockets


* https://www.facebook.com/note.php?note_id=389414033919
