# Assassination System — Unreal Engine 5

A modular stealth/melee assassination system triggered via sphere trace detection. Designed to be plug-and-play with minimal setup — just add your animations and tune two values to match your game's scale.

## What it does
Press **E** near a valid target to trigger a context-sensitive assassination sequence. The system uses a sphere trace combined with a dot product angle check to detect whether the target is within range and facing the correct direction (e.g. behind/unaware) before allowing the execution to fire.

## Features
- Sphere trace-based target detection on input (E key)
- Dot product check to validate approach angle (front/back detection for stealth kills)
- Fully scalable — trace radius and angle threshold are exposed and adjustable
- Drop-in animation slots for player and target
- Blueprint-driven, easy to extend to additional enemy types

## How it works
1. On pressing **E**, a sphere trace is fired from the player to detect nearby valid targets within range.
2. A dot product check compares the player's forward vector against the vector to the target (or the target's forward vector, depending on your setup) to confirm valid approach angle — e.g. only allowing a backstab if the dot product falls below a set threshold.
3. If both checks pass, the system triggers the assassination montage on both the player and the target, syncing position/rotation for the kill animation.
4. On animation completion, the target is destroyed/disabled and control returns to the player.

## Setup — Scalability
This system ships without animations by default. To get it fully working:

1. **Add two animation montages:**
   - Player assassination montage (the kill animation)
   - Target death/reaction montage (synced to the player's animation)
2. **Adjust the dot product threshold** in the detection logic to control how strict the approach-angle requirement is (e.g. -0.5 to -1.0 for strictly-behind detection, adjust based on your game's feel).
3. **Adjust the sphere trace radius** to match your game's scale — smaller for tight melee ranges, larger for more forgiving detection.

Both values are exposed as variables, so no code/blueprint restructuring is needed — just tune to fit your project.

## Tech
Unreal Engine 5 · Blueprints · Sphere Trace · Vector Math (Dot Product)

## Demo
[Add a short gameplay clip or GIF here]

## Notes
- Detection logic is intentionally decoupled from animation so you can reskin this for any character/enemy type.
- Consider adding a line-of-sight trace alongside the sphere trace if you want to block assassinations through walls.
