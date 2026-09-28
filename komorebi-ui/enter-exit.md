# Enter and exit animations

Staged entrances and exits for moments where sequence or spatial continuity helps.

Interactive state feedback lives in [animations.md](animations.md); icon swaps in [icon-transitions.md](icon-transitions.md).

## Entrance is not a default page treatment

A page does not need to prove that it loaded by animating every section.

Use staged entrance only when the sequence itself carries meaning:
- a first reveal;
- a meaningful success;
- a composed empty state;
- an intentional narrative / editorial moment.

Routine pages, settings, repeated tabs and high-frequency work surfaces should normally appear settled.

## Split by meaning, not by visual novelty

When staging an entrance, animate semantic groups:
- title;
- supporting copy;
- main action;
- focal media.

Do not split every word or letter unless the typography itself is the subject of the moment.

Word-by-word stagger is expressive editorial motion, not a default polish recipe.

## Stagger follows hierarchy

If elements genuinely need sequence, use a small stagger that makes the order readable without turning the page into a performance.

Use the project's established timing first.

A useful quiet starting point is roughly `40–80ms` between semantic groups, then verify at normal speed. Larger staggers can fit ceremonial or narrative moments but should be rare.

## Movement should follow the scene

A fixed `translateY(12px)` is one recipe, not a law.

Choose direction from the relationship:
- item rises from below because it was revealed under something;
- panel enters from the side it is spatially attached to;
- object expands from its origin;
- content fades in place when no spatial story exists.

Do not introduce movement when opacity alone explains the change.

## Continuity from the current state

Never reset to a canonical start pose just so an entrance animation can play.

If an object is already visible, partially open, scrolled or positioned, continue from that truth.

The previous frame still counts.

## Exits recede unless direction matters

Exit motion usually asks for less attention than entry.

Options:
- immediate removal;
- opacity fade;
- small spatial movement;
- full spatial return when destination / origin matters.

Use full-slide exits for drawers, cards returning to a list or objects whose spatial destination explains the interaction.

Do not add direction merely because every exit “should move somewhere”.

## Duration

Do not hardcode one global enter/exit duration into the design language.

Duration depends on:
- distance;
- element size;
- frequency;
- input modality;
- whether the movement carries information.

Short / local transitions should finish quickly. Larger spatial movements may take longer.

The animation should feel complete without making the user wait.

## Reduced motion

The state must remain understandable without the motion.

When reduced motion is requested, remove nonessential movement and preserve the final static state, labels, icons and hierarchy.

## Verification

Check:
- first render;
- repeat entry;
- reverse / close before enter completes;
- keyboard activation where relevant;
- previous state continuity;
- reduced motion;
- whether the entrance still feels acceptable on the fiftieth encounter.

If the user starts waiting for the entrance, it is too much.
