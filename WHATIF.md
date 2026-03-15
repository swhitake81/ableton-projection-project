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
