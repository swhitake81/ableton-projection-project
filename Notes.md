# Fun Notes - things i write as i learn

## Quotes

"Every 'declarative' language eventually becomes a (terrible) programming language just without the aid of actual language design."

- Brian Goetz (Java Architect)

## Notes

### OSC

OSC, or OpenSoundControl, is a data transport specification for realtime message communication among applications and hardware. "OSC can be understood as a more flexible alternative to MIDI".

#### Questions

#### Sources

https://opensoundcontrol.stanford.edu/

### Pkl

Pkl doubles as a programming language and a configuration language.

#### Sources

https://www.youtube.com/watch?v=dj-nspfpX_A

#### How it works

You can think of a `.pkl` file as a single `{}` situation in `.json`

If I had a file `bar.pkl` that consisted of this:

```pkl
foo = 1

bar = foo

nested {
    prop = 1
}
```

Then ran `pkl eval bar.pkl -f json`, my result would be:

```json
{
  "foo": 1,
  "bar": 1,
  "nested": {
    "prop": 1
  }
}
```

#### Demo

We have a config file, _*myConfig.yaml*_, which has some basic set up for deployment settings.

```yaml
machines:
  - region: us-west
    env:
      http_proxy: proxy.us-west.ex
    cpus: 4
    memory: 4Gi
    healthchecks:
      - port: 4050
        type: TCP
        interval: 5
  - region: us-east
    env:
      http_proxy: proxy.us-east.ex
    cpus: 4
    memory: 4Gi
    healthchecks:
      - port: 4050
        type: TCP
        interval: 5
```

And here's how we'd create the same file using Pkl. We start with defining a module:
_*FooBarSystem.pkl*_

```pkl
module FooBarSystem

machines: Listing<Machine>

class Machine {
    region: "us-west"|"us-east"

    env: Mapping<String, String>

    cpus: UInt8

    memory: DataSize(this < 1.tib)

    healthchecks: Listing<Healthcheck>

    @SourceCode { language = "Bash" }
    startScript: String?
}

class Healthcheck {
    port: UInt16
    type: "TCP"|"HTTP"|"HTTPS"
    interval: Duration
}

output {
    renderer = new YamlRenderer {
        converters {
            [DataSize]= (it) ->
               let (unit = it.unit.dropLast(1).capitalize())
                "\(it.value)\(unit)"
            [Duration] = (it) -> it.toUnit("min").value
        }
    }
}
```

Then here is where we actually define a the new config file from the template:
_*myConfig.pkl*_

```pkl
amends "FooBarSystem.pkl"

local baseMachine: Machine =
    new {
        env {
            ["http_proxy"] = "proxy.\(outer.region).ex"
        }
        cpus = 4
        memory = 4.gib
        healthchecks {
            new {
                port = 4050
                type = "TCP"
                interval = 5.min
            }
        }
    }

machines {
    (baseMachine) {
        region = "us-west"
    }
    (baseMachine) {
        region = "us-east"
    }
}
```

Running `pkl eval myConfig.pkl` should be the same.

#### Questions

1. Does `DataSize` have a set format?

- You can edit output to whatever format you'd like with "converters" convention in pkl scripts.
