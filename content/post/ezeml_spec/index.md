---
title: "EZPT Exercise Markup Language (EZEML)"
description: "EZEML is a simple, verbose, backwards compatible, markup language to describe a workout. "
slug: "ezeml"
date: 2022-09-22 00:00:00+0000
#image:
tags:
    - "Swift"
keywords:
    - "EML"
    - "EZEML"
weight: 1
---

This document is from my work at [ezpt.xyz](https://www.ezpt.xyz/), where I worked as an iOS developer on their physical therapy application. My hope is that this language becomes an industry standard, or at least a stepping-stone for the future of exercise notation.

## Why are we creating EZEML?

Workouts (aka Routines) on our app are constantly changing. Every time we modify what a workout looks like, we have to change our entire database schema. This is a difficult operation. With EZEML, our client-side app simply has to implement a version of EZEML that is high enough to run the current features. Existing workouts will not have to be migrated. The language will also be able to generate a human-readable description of the workout.

## What constructs does EZEML v1 implement?

- Sets & Reps
- Drop/Pyramid/Ladder sets
- Supersets/Circuits
- Asymmetric (Unilateral) exercises (Ex: single leg RDL)
- Weight, Time-based, RPE/ORM, Failure sets

## Syntax

This section will introduce EZEML in increasing levels of complexity with examples before giving a technical definition.

| Description | EZEML |
|---|---|
| 5 sets of 5 squats | `"squat":5x5` |
| 3 sets of squats to failure | `"squat":3xF` |
| 3 sets of squats with reps of 4, 6, and 8 | `"squat":3x(4,6,8)` |
| 3 sets of 8 squats with the last set to failure | `"squat":3x(8,8,F)` |
| 2 sets of 8 reps bench at 125lbs | `{"weight":lbs}"bench":2x8@125` |
| 3 sets of 8 reps decreasing by 3 bench at 125lbs | `{"weight":lbs}"bench":3x(8,5,2)@125` |
| Dropset of 4 sets, 4 reps, starting at 225lbs, drop by 15lbs deadlift | `{"weight":lbs}"deadlift":4x(4@225,4@210,4@195,4@180` |
| Dropset of 4 sets, 4 reps increasing by 3, starting at 90lbs, drop by 15lbs overhead press | `{"weight":lbs}"overhead-press":4x(4@90,7@75,10@60,13@45)` |
| 3 sets of 4 reps single leg RDL’s | `"single-leg-rdl":3x4:3x4` |
| 3 sets of 4 reps on left leg, 3 sets of 5 reps on right leg, single leg RDL’s | `"single-leg-rdl":3x4:3x5` |
| 3 sets of 5 squats, 3 sets of 5 deadlift | `"squat":3x5;"deadlift":3x5` |
| 4 sets of 10 overhead press, and superset of 3 sets of 5 squats, 3 sets of 5 deadlift. | `"overhead-press":4x10;super("squat":3x5;"deadlift":3x5)` |
| 4 sets of 60sec achilles iso hold | `"achilles-iso":4x60T` |
| 4 sets of 60, 80, 100, 120 sec, achilles iso hold | `"achilles-iso":4x(60T,80T,100T,120T)` |
| 4 sets of 60 sec achilles iso hold with 40lbs | `{"weight":lbs}"achilles-iso":4x(60T)@40` |
| 4 sets of 60 sec decreasing by 10sec achilles iso hold with 40lbs increasing by 10lbs | `{"weight":lbs}"achilles-iso":4x(60T@40,50T@50,40T@60,30T@70)` |
| 4 sets of 60sec single leg achilles iso hold | `"single-leg-achilles-iso":4x60T:4x60T` |
| 4 sets of 5 squats at 6 RPE | `"squat":4x5%6` |

EZEML v1.0 is made up of two sections, the header and the tokens (body.)

### Syntax: The Header

The header is used for creating context for the computer. It can be omitted if you are using this notation by hand. Parameters are delimited by commas. You may also pass in key-value pairs not enumerated by this specification to be used in your implementation.

Parameters:
- *required* `version`: The version of EZEML it was written in.
- *required* `weight`: The unit of weight for all the exercises. Supported weights: lbs (Pounds), kg (kilograms), st (stone).
- `rest-set`: The amount of rest between sets (seconds)
- `rest-exercise`: The amount of rest between exercises (seconds). Behavior of this parameter when it comes to supersets is left to the implementation.
- `name`: The name for the workout. Workouts do not have to be named.

Example: `{"version":"1.0","weight":"lbs","rest-set":30,"rest-exercise":60,"name":"Strength program 2"}`

### Syntax: The Body

A token is an exercise within a workout. They are separated by “;”. There are two types of tokens: Single, and Super. There is also a Circuit token, which is an alias of Super. Single is a single exercise. Super is a collection (superset) of tokens (other exercises) - however these tokens have the restriction of no supersets, since EZEML v1.0 prohibits nested supersets. A Single token has two parts, name and work - separated by “:”. The name is the name of an exercise. The work is what you’ll be doing for that exercise. Names follow naming conventions in Rules (next section.) Work can further be separated by another “:” in certain cases (asymmetric exercises). A Super token surrounds a collection of Single tokens with function-like syntax `super(...)`. A Circuit is the same as a Super, it is a generalized grouping of exercises, while a superset is usually designed with a “push pull” aspect.

| Type | Description | Syntax |
| --- | --- | --- |
| Single | A single exercise with a name and work. | `"NAME":WORK` |
| Super | A collection of other tokens | `super(SINGLE;...)` |
| Circuit | A collection of other tokens | `circuit(SINGLE;...)` |

There are 4 kinds of work: None, Standard, Standard Varied, Asymmetric.

| Kind | Description | Syntax |
| --- | --- | --- |
| None | No Work. | |
| Standard | SETS and REPS delimited by “x”. | `SETSxREPS` |
| Standard Varied | SETS and (variable) REPS delimited by “x”. | `SETSx(REPS,...)` |
| Asymmetric | A standard or standard varied or none kind on each side of “:” delimiter. | `STANDARD:STANDARD` or `STANDARD:STANDARD_VARIED` or `STANDARD:NONE` or `STANDARD_VARIED:STANDARD` or `STANDARD_VARIED:STANDARD_VARIED` or `STANDARD_VARIED:NONE` or `NONE:STANDARD` or `NONE:STANDARD_VARIED` or `NONE:NONE` |

Reps can have modifiers attached to them. Modifiers follow a precedence, and should be applied top to bottom in the following chart. RPE cannot be combined with weight, but it can be combined with time.

| Modifier | Description | Syntax |
| --- | --- | --- |
| Time | Makes reps be time-based instead of repetition based. | `REPST` |
| Weight | Designates how much weight you should be lifting for a given rep. | `STANDARD@WEIGHT` or `STANDARD_VARIED@WEIGHT` or inside `STANDARD_VARIED` like `SETSx(REPS@WEIGHT,...)` aka `REPS@WEIGHT` |
| RPE | Designates the intensity of the rep. | `STANDARD@RPE` or `STANDARD_VARIED@RPE` or inside `STANDARD_VARIED` like `SETSx(REPS@RPE,...)` aka `REPS@RPE` |

## Rules (Not exhaustive)

- Acceptable characters for naming (workouts and exercises): a-z, A-Z, " “, “-”, 0-9, “’”, “,”, “:”, “%”, “°”, “+”, “/”, “&”, “@”, “<”, “>”, “#”, “(”, “)”.
- You cannot currently put a superset inside of a superset
- If you modify weight for one set, you must explicitly set it for the other sets too
- If a symetrical exercise has an asymetrical/unilateral variation (RDL’s, single leg RDL’s), you should not use asymetrical notation on the symetric version. All named exercises have a concrete description. While a single arm bench might exist, you should name it “single-arm-bench” (or something else) instead of “bench”.
- Time must be notated in seconds. (Ex: 1 minute and 20 seconds -> 80sec)
- Time sets may not be combined with rep sets. This goes back to “all named exercises have a concrete description” point. You may however superset a rep set and a time set for a similar effect.
- The max number for reps, sets, weight, and time, is currently 65535.
- Fractional weight is accepted up to 2 decimal places.
- Exercise names have a minimum length of 1 and max of 128 characters (Ex: *nathans-super-epic-amazing-special-exercise-with-some-awesomely-cool-modifications-and-a-super-long-name-that-has-128-characters*.)
- Supersets must have 2 or more exercises
- STANDARD_VARIED SETS and number of REPS terms must match (Ex: 3x(4,4,4) *right*, 3x(4,4) *wrong*.)

## Parsing

EZEML is simple enough that you don’t need node trees or other data structures. However, the implementation is your choice. You can parse all tokens at once, or parse “by the wire,” one token at a time (iterating over the lexemes) - however depending on the source of your EZEML files you may need to call a validation function to ensure the syntax is correct.

## Files & Compression

A file should contain a single workout. The file extension is *.ezml*. EZEML is meant to be human readable, however you are free to add a layer of abstraction and add lossless compression if you wish. We suggest you use the file extension *.ezmlc* for compressed EZEML.

## FAQ

- **How do I notate ROM?** EZEML does not currently support ROM. Create separate exercises for different ROM. (Ex: “squat-parallel”, “squat-atg”)
- **How do I notate tempo?** EZEML does not currently support tempo. Create separate exercises for different tempo. (Ex: “bench-4-2-1”). You could also make a timeset with weight - which works well for eccentric exercises.
- **How do I notate negatives?** Negatives are considered separate exercises than their “positives” counterparts, so just name them differently (Ex: “neg-bench”)
