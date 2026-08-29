# PieLocator

A client-side Minecraft mod that experiments with the information exposed through Minecraft's debug profiler / pie chart.

The idea is pretty simple:

**Minecraft already gives the client profiler information. What happens if we actually analyze it?**

PieLocator attempts to use changes in profiler data while moving around to estimate the location of certain client-observable entities and block entities.

> ⚠️ **This is an experimental project.**
>
> The results are estimates and aren't guaranteed to be accurate. Don't use it on multiplayer servers if it violates their rules.

## How it works

When you activate the scanner, PieLocator collects a baseline of the profiler data and then guides you through a few measurements.

For example:

```text
Scanning...

Move 5 blocks → EAST

[██████░░░░] 60%

Take another measurement...
```

The mod can repeat this process from different positions and compare the measurements.

The general idea is:

```text
        Target
           ●
          /
         /
        /
       /
      ●
   Position 2

 ●
Position 1
```

By combining multiple observations, the mod can narrow down a probable area instead of trying to get an exact coordinate from a single measurement.

The scanner can also assist with camera direction while collecting measurements.

## Features

* Client-side keybind to open the scanner
* GUI for selecting a target type
* Profiler/pie-chart data analysis
* Guided movement measurements
* Automatic camera direction assistance
* Estimated XYZ coordinates
* Confidence / accuracy estimate
* Supports selected entities and block entities
* No server-side plugin required

## Example

You select a target and start scanning:

```text
┌──────────────────────────────┐
│          PIELOCATOR          │
├──────────────────────────────┤
│ Target: Chest                │
│                              │
│ Scanning...                  │
│                              │
│ → Move 5 blocks EAST         │
│                              │
│ Measurement 2 / 5            │
└──────────────────────────────┘
```

After enough measurements:

```text
TARGET ESTIMATED

Chest

X: 1247
Y: 63
Z: -382

Estimated error: ±2 blocks
Confidence: 94%
```

The numbers above are just an example.

## Why?

The Minecraft debug pie chart is usually treated as a performance/debugging tool.

This project is basically me asking:

> "What other information can be extracted from it?"

PieLocator is intended to be a technical experiment into Minecraft's client-side profiling behavior and how seemingly harmless debug information can potentially be correlated with player movement.

## Compatibility

Currently targeting:

* Minecraft: `1.21.x`
* Loader: `Fabric`

Other versions may work, but profiler internals change between Minecraft versions.

## Installation

Install the required Fabric Loader and Fabric API for your Minecraft version, then place the PieLocator `.jar` into your `mods` folder.

## Multiplayer

PieLocator is **client-side**, but that doesn't mean every server will consider it fair to use.

Some servers may consider tools like this an exploit or an unfair advantage.

**Check the server's rules before using it.**

## Limitations

This isn't a magic radar.

Accuracy depends on things such as:

* Minecraft version
* Profiler behavior
* Client tracking/render distance
* Target type
* Server implementation
* Player movement
* Measurement accuracy
* Other profiler activity

The scanner can therefore produce false positives or inaccurate coordinates.

## Development

This project is mainly an experiment, so expect things to break.

If Minecraft changes the profiler again, there's a good chance parts of the scanner will need to be rewritten.

Pull requests and technical discussion are welcome.
