What if I could generate Ableton projects in VS code?
Like I live built a scaffolding for a beat template.
What if it /didn't/ use Max for Live?
What if it went something like this

## code

```
def device.drum_buss(): instantiates drum buss with sounds from ~/Desktop/sounds/

on start:
  channel_1:
    - chain: [drum_buss, saturator]
      vol: 6
      to: [main, send_1]
```

This yaml-like structure is good for templatizing sessions as well as live rendering.
How does the app know it's ok to communicate with a particular folder?
It doesn't communicate with folders or directories. It communicates with Ableton Live.
Program has ability to communicate with Ableton Live threads to change data in real time.
Sonic Pi or other music live coding language to create midi or audio loops in Session and Arrangment View.

[Would Pkl be a good candidate for this instead of yaml?](https://www.youtube.com/watch?v=dj-nspfpX_A_)

## how Sonic Pi communicates using OSC

At launch, Sonic Pi listens on 4560 for OSC msgs.

The format for a message is like this in Sonic Pi's logger: `/osc:127.0.0.1:4560/hello/world`

This is how to send a message externally within Sonic Pi's editor:

```
use_osc "localhost", 123456
osc "/hello/world"
```

In this case we're assuming there's another program on the same machine
listening to port 123456. If there is, then it will receive a
`"/hello/world` OSC message with which it can do what it wants.

Sonic Pi can also send messages to external hosts. But it cannot receive from external hosts by default.

"By default when Sonic Pi is launched it listens to port 4560 for
incoming OSC messages from programs on the same computer. This means
that without any configuration, you can send Sonic Pi an OSC message and
it will be displayed in the cue log just like incoming MIDI
messages. This also means that any incoming OSC message is also
automatically added to the Time State which means you can also use `get`
and `sync` to work with the incoming data - just like with MIDI and
synchronising `live_loops` - see sections 5.7 and 10.2 to recap how this
works."

"We can send OSC to Sonic Pi from any programming language that has an
OSC library. For example, if we're sending OSC from Python we might do
something like this:

```
from pythonosc import osc_message_builder
from pythonosc import udp_client

sender = udp_client.SimpleUDPClient('127.0.0.1', 4560)
sender.send_message('/trigger/prophet', [70, 100, 8])
```

"

## Resources

### Ableton Live programmatic control

- https://github.com/ideoforms/AbletonOSC — community remote script that exposes Live's API over OSC, **no Max for Live required**. Could be the key to real-time control without M4L.
- https://ableton.github.io/export/ — official C++ library for writing .als (Ableton Live Set) files programmatically. Write-only, no live interaction — useful for scaffolding/generating session templates.

### Ableton + Max for Live

- https://www.ableton.com/en/packs/connection-kit/ — Ableton Connection Kit (uses M4L)
- https://github.com/Ableton/m4l-connection-kit — source for the above

### Config languages

- https://www.youtube.com/watch?v=dj-nspfpX_A — Pkl overview video

### OSC

- https://opensoundcontrol.stanford.edu/ — OSC spec
