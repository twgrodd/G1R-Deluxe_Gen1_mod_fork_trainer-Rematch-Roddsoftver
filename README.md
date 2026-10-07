# Trainer Rematch RoddSoft

Talk to any trainer you have already beaten and they challenge you to a rematch, with a YES/NO prompt. Supports Generation 1 (Red/Blue/Yellow) and Generation 2 (Gold/Silver/Crystal).

## About the RoddSoft fork

**Trainer Rematch RoddSoft** is a maintained fork of the original Trainer
Rematch mod, expanded for G1R Deluxe / Gen1Recomp players who want rematches
without sacrificing normal story progression.

The fork keeps the original idea -- talk to a trainer you have already beaten
to fight them again -- while extending it across both generations, adding more
control over rematch rewards and teams, and protecting story-critical
post-battle interactions. The goal is for the mod to feel like an optional
gameplay feature rather than something that changes or blocks the base game's
progression.

### What this fork adds and improves

- **Full Gen 1 and Gen 2 support** -- Red/Blue/Yellow and
  Gold/Silver/Crystal are supported by the same mod.
- **Gym Leader, Elite Four, Champion and boss rematches** -- supported
  defeated major trainers can be challenged again once their required story
  interaction is complete.
- **Dedicated rematch teams** -- trainer data can provide a `rematchIndex`,
  allowing compatible projects such as Yellow Legacy Changes to supply a
  purpose-built rematch team instead of simply replaying the original party.
- **Configurable rematch rewards** -- the MODS menu provides separate
  0-100% controls for prize money and EXP in 10% steps. Money defaults to 0%
  and EXP to 100%; Pay Day remains disabled during rematches.
- **Class-specific dialogue** -- trainer classes have their own rematch
  challenges, decline reactions and stronger-team warnings rather than a
  single generic prompt.
- **Level-gap warning** -- if the rematch team averages more than 10 levels
  above your party, the trainer warns you and asks for confirmation again.
- **Gen 2 story protection** -- progression-critical post-battle dialogue
  takes priority over rematches. This includes Gym Leaders that still owe a
  badge or TM and the Team Rocket grunts in the Mahogany HQ whose dialogue
  reveals the required passwords.
- **Gen 1 story protection** -- known progression-sensitive trainer
  interactions keep priority over rematches. The Fighting Dojo Karate Master,
  for example, keeps his reward interaction until Hitmonlee or Hitmonchan has
  actually been chosen.
- **Rocket Hideout Lift Key compatibility** -- the mod requires a
  Gen1Recomp version containing the corrected Lift Key battle-completion
  handling, preventing a rematch interaction from breaking that required
  progression item.
- **Safer save compatibility** -- the fork does not add its own save data;
  normal saves continue to work with the mod enabled or disabled.

### Why the story safeguards matter

A defeated trainer is not always finished with the player when the battle
ends. Some Pokémon scripts use the trainer's next conversation to award a
badge, TM, Pokémon, password or other progression result. A rematch mod that
blindly replaces every defeated-trainer conversation can therefore make the
game impossible to progress without disabling the mod.

This fork treats those interactions as higher priority than a rematch. When a
known story action is still pending, the original game conversation runs
normally. After the relevant reward or progression event has been completed,
the trainer becomes available for rematches. Regression coverage is included
for these safety rules, including the Gen 2 Mahogany password flow and the
Gen 1 Fighting Dojo reward flow.

For the detailed version-by-version history, see [CHANGELOG.md](CHANGELOG.md).

## How it works

1. Beat a trainer, then walk up and talk to them again.
2. They greet you with a line written for their class (each class speaks in the voice it uses in its regular dialogue, including all Johto Gym Leaders, Elite Four, Champions, and Johto/Kanto trainer classes).
3. Answer the prompt:
   - **YES** - battle them again. Rematch earnings are a **percentage of the usual amounts**, set in MODS > Trainer Rematch: **REMATCH MONEY %** (default 0%) and **REMATCH XP %** (default 100%), each a 0-100% slider in 10% steps. Pay Day stays disabled on rematches.
   - **NO** - they react in character: cocky classes mock you for being scared, wise ones are understanding. Their normal post-battle line still follows, so nothing from the base game is lost.

If the rematch team averages **more than 10 levels above your party**, they warn you first in their own voice and ask again — say YES to battle anyway, or NO to walk away.

Gym leaders, rivals and other scripted encounters keep their original conversations. A Gym Leader only starts offering rematches once they have nothing left to hand over: beating them in Gen 2 only sets the "beaten" flag, and the badge (and often their TM) comes from their own talk afterwards, so that talk is theirs until the badge and TM are in your hands. A class which marks a dedicated rematch team (a `rematchIndex` in its trainer record, like the Yellow Legacy Changes mod ships for the gym leaders, Elite Four and Champion) uses that team for the rematch instead of the trainer's own party.

## Try it

1. Install the mod into your game's `mods/` folder (or drop the zip in via the launcher).
2. Restart the game and enable the mod if it is not on.
3. Beat a field trainer (a Youngster, Bug Catcher, Lass, Schoolboy...), then talk to them again.

## What changed

- `manifest.json` - targets `"games": ["gen1", "gen2"]` for full Gen 1 and Gen 2 engine coverage.
- `main.lua` - wraps the overworld talk flow across Gen 1 and Gen 2 engines to offer rematches, handles Gen 2 NPC structures and trainer scripts, scales money and experience in rematch battles from the MODS-menu percentages, and defines trainer lines for all Gen 1 and Gen 2 classes. No save changes; your file works with or without the mod.
