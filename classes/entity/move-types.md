---
description: Table with move types an their values
---

# Move types

Read more about move types [here](https://developer.valvesoftware.com/wiki/MoveType)!

<table><thead><tr><th>Name</th><th data-type="number">Value</th><th>Description</th></tr></thead><tbody><tr><td><code>MOVETYPE_NONE</code></td><td>0</td><td>Freezes the entity, outside sources can't move it</td></tr><tr><td><code>MOVETYPE_ISOMETRIC</code></td><td>1</td><td>For players in TF2 commander view etc. Do not use this for normal players!</td></tr><tr><td><code>MOVETYPE_WALK</code></td><td>2</td><td>Default <a href="https://developer.valvesoftware.com/wiki/Player">player</a> (client) move type</td></tr><tr><td><code>MOVETYPE_STEP</code></td><td>3</td><td>NPC movement</td></tr><tr><td><code>MOVETYPE_FLY</code></td><td>4</td><td>Fly with no gravity</td></tr><tr><td><code>MOVETYPE_FLYGRAVITY</code></td><td>5</td><td>Fly with gravity</td></tr><tr><td><code>MOVETYPE_VPHYSICS</code></td><td>6</td><td>Physics movetype (prop models etc)</td></tr><tr><td><code>MOVETYPE_PUSH</code></td><td>7</td><td>No clip to world, but pushes and crushes things</td></tr><tr><td><code>MOVETYPE_NOCLIP</code></td><td>8</td><td>Noclip, behaves exactly the same as console command</td></tr><tr><td><code>MOVETYPE_LADDER</code></td><td>9</td><td>For players, when moving on a ladder</td></tr><tr><td><code>MOVETYPE_OBSERVER</code></td><td>10</td><td>Spectator movetype. DO NOT use this to make player spectate</td></tr><tr><td><code>MOVETYPE_CUSTOM</code></td><td>11</td><td>Custom movetype, can be applied to the player to prevent the default movement code from running, while still calling the related hooks.</td></tr></tbody></table>
