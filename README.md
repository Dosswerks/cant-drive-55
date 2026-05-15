# Can't Drive 55

*One foot on the brake and one on the gas.*

Can't Drive 55 is a pseudo-3D arcade driving game inspired by Sega's OutRun and Atari's Pole Position. The player drives the band to their next gig across a winding California highway, dodging police cruisers and roadside obstacles while the speedometer climbs past the legal limit. The game is a promotional tie-in for the Atlanta-based Sammy Hagar tribute band Can't Drive 55.

---

## Gameplay

The car accelerates automatically. The player's only job is to steer left and right to stay on the road, navigate curves, and dodge traffic. The game features two playable tracks:

- **Day Drive**: The classic California highway — golden hills, blue sky, and police cruisers to dodge.
- **Night Drive**: A neon-lit city drive through nighttime Atlanta — more traffic, tighter curves, and a completely different atmosphere.

The drive is broken into 3 miles. Complete each mile and you get 30 more seconds on the clock. Make it through all 3 miles and the band makes it to the gig.

## Title Screen

The title screen features two steering wheel buttons for track selection:
- **DAY DRIVE** — yellow pulsating glow
- **NIGHT DRIVE** — red pulsating glow

The glows alternate on a 1-second cycle. An attract mode demo plays automatically after idle time, alternating between the day and night tracks.

## Controls

- **Desktop**: Left and right arrow keys to steer. R to restart. Q to quit to title screen.
- **Mobile**: Slide your finger left and right — finger position directly controls the car.

## Difficulty Progression

### Day Track
- The first stretch of road has no police cars — just curves and scenery to get comfortable with the steering.
- Police cars spawn gradually as you drive further. The first one appears after a long warm-up period.
- Gaps between cop spawns shrink over time, up to a maximum of 8 cops on the road.
- Road curves start gentle and get progressively tighter deeper into the track.

### Night Track
- Higher spawn frequency — cars appear more often and more quickly.
- Up to 12 vehicles on the road simultaneously.
- Tighter, more frequent curves (city driving feel).
- Three enemy types with different behaviors (see Obstacles below).

## Obstacles

### Day Track
- **Police Cars**: Appear on the road ahead. Collision costs a life, resets the player to the start of the track, and clears nearby cops. New cops respawn further ahead.

### Night Track
- **Police Cars** (10% of spawns): Same collision behavior as day. Feature alternating red and blue flashing glow points on top.
- **Blue Sports Cars** (55% of spawns): Weave more aggressively across lanes. Unique pass sound.
- **Yellow Taxis** (35% of spawns): Drift more slowly and predictably. Unique pass sound.

### Both Tracks
- **Billboards**: Six different band photo billboards line both sides of the road. Driving off the road into a billboard causes a crash.
- **Speed Limit Signs**: "55" signs appear periodically on both sides. Hitting one causes a crash.
- **Off-Road**: Driving past the rumble strips triggers a slowdown, screen shake, and off-road sound. Day track shows dust; night track shows sparks.

## Night Track Visual Features

- **Atlanta skyline background**: Night sky photo of the Atlanta skyline
- **Neon road markings**: All lane stripes and center line glow yellow
- **Road borders**: Alternating white and dark grey
- **Streetlights**: Vertical poles on both sides of the road with glowing lamps and spotlight cones shining down onto the road surface
- **Billboard spotlights**: Radial light cones illuminate each billboard from below, with neon glow borders
- **Brake lights**: Red glow points with halos on the rear of all vehicles (player and enemies)
- **Police flashers**: Alternating red/blue glow points on cop cars
- **Aircraft**: Points of light (blinking red or white) fly across the sky in straight lines — planes and helicopters creating a buzz of city activity
- **Speed lines**: Blue-tinted at night (white during day)
- **Dark road surface and shoulders**: City asphalt feel
- **No player car shadow** (removed for night realism)

## Game Over Conditions

- **REVOKED!** — Lose all 5 lives. A fake driver's license image appears above the text.
- **TIME'S UP!** — Timer reaches zero. A custom image appears above the text.
- **YOU MADE IT!** — Complete all 3 miles. The band logo appears above the text.

## HUD Elements

- **Speedometer**: Chrome-bordered analog gauge in the upper center of the sky. Dark face with grey notches, red needle, and mph readout inside the circle. Color-coded arc (green/yellow/red). Max speed is 125 mph.
- **Lives Left**: Upper-left corner shows remaining lives as tiny car icons with a "LIVES LEFT:" label.
- **Band Logo**: Upper-right corner displays the band's logo.
- **Time Left / Mile Counter**: Top bar shows remaining time and current mile progress.

## Crash & Recovery

When the player hits a vehicle, billboard, or sign:
- A 2-frame explosion sprite replaces the car for 1.5 seconds
- Speed drops to zero
- Player resets to the start of the track
- Nearby cars are cleared and new ones spawn further ahead
- Crash sound plays, plus game over sound if it was the final life

---

## The Story

The band is loaded up and the next gig is across town — but the clock is ticking. Doors open in an hour, the promoter is calling, and the only thing between you and the stage is a long stretch of open highway.

You are behind the wheel. The gear is in the back. The setlist is ready. All you have to do is get there. But the speed limit says 55, and you just cannot follow it.

*"Go on and write me up for 125. Post my face, wanted dead or alive. Take my license, all that jive — I can't drive 55."*

---

## Technical Details

### Architecture

Can't Drive 55 is a single-file HTML5 Canvas game with no external dependencies (aside from the QR code library for the tip jar). All game logic, pseudo-3D road rendering, audio management, and input handling are contained in one `index.html` file. It runs in any modern browser on desktop or mobile.

### Social Sharing

The page includes Open Graph and Twitter Card meta tags for rich link previews when shared on social media. The `box-art.png` asset is used as the preview image.

### Key Technical Features

- **Pseudo-3D road rendering**: Perspective-projected road segments with curves, hills, shoulders, rumble strips, and lane markings
- **Dual track system**: Day and night modes with independent track layouts, color palettes, and enemy configurations
- **Multiple enemy types**: Cops, sports cars, and taxis with distinct drift behaviors and pass sounds
- **Night mode lighting**: Streetlights with spotlight cones, billboard spotlights, brake light glows, police flashers, and neon road markings
- **Aircraft system**: Blinking points of light crossing the night sky
- **Parallax scrolling**: Two-layer hills and horizon buildings shift with steering for depth (day track)
- **Dynamic traffic spawning**: Progressive difficulty that ramps naturally based on distance traveled
- **Roadside scenery**: Billboards and signs scale with perspective and support custom images
- **Analog speedometer**: Chrome-bordered gauge with notches, colored arc, and red needle
- **Explosion sprites**: 2-frame animated explosion on crash
- **Off-road effects**: Slowdown, screen shake, dust/sparks overlay, and sound
- **Speed lines**: Visual streaks at high velocity (white day, blue night)
- **Attract mode**: Alternates between day and night track demos with AI driving
- **Responsive layout**: Canvas scales to fit mobile screens
- **Touch controls**: Finger-position steering for mobile
- **Tip jar**: PayPal donation button with QR code, consistent with other Dosswerks Arcade games

### Asset System

All custom assets are defined in config objects at the top of the script:

```javascript
// Day mode assets
const A = {
    playerCarImage: 'assets/player.png',       // 250x155 rear view
    enemyCarImage: 'assets/enemy.png',         // police car rear view
    backgroundImage: 'assets/sky.png',         // 640x216 sky background
    boxArtImage: 'assets/box-art.png',         // splash screen / OG image
    billboard1Image–billboard6Image,            // band photo billboards
    signImage: 'assets/sign.png',              // speed limit sign
    horizonImage: 'assets/horizon.png',        // parallax horizon strip
    bandLogoImage: 'assets/band-logo.png',     // 60x80 upper-right corner
    livesCarImage: 'assets/lives-car.png',     // tiny car for lives display
    explosion1Image: 'assets/explosion1.png',  // explosion frame 1
    explosion2Image: 'assets/explosion2.png',  // explosion frame 2
    licenseImage: 'assets/license.png',        // game over (REVOKED)
    timesUpImage: 'assets/timesup.png',        // game over (TIME'S UP)
    crashSound, passSound, lapSound, offRoadSound,
    backgroundMusic, gameOverSound, winSound,
    sportsPassSound: 'assets/sports-pass.mp3', // sports car pass sound
    taxiPassSound: 'assets/taxi-pass.mp3',     // taxi pass sound
};

// Night mode assets (overrides)
const AN = {
    playerCarImage: 'assets/night-player.png',   // 250x164 rear view
    enemyCarImage: 'assets/night-enemy.png',     // night police car
    sportsCarImage: 'assets/night-sports.png',   // blue sports car
    taxiCarImage: 'assets/night-taxi.png',       // yellow taxi
    backgroundImage: 'assets/night-sky.png',     // Atlanta skyline photo
    backgroundMusic: 'assets/night-music.mp3',   // night track music
};
```

Any missing file falls back to a placeholder graphic or no sound.

### File Structure

```
cant-drive-55/
  index.html          — game + all logic
  story.html          — backstory and instructions
  README.md
  assets/
    player.png        (250x155)
    enemy.png
    sky.png           (640x216)
    box-art.png       (splash + OG share image)
    wheel.png         (100x114, title screen buttons)
    billboard1–6.png
    sign.png
    horizon.png       (640x60)
    band-logo.png     (60x80)
    lives-car.png
    explosion1.png    (250x155)
    explosion2.png    (250x155)
    license.png       (200x120)
    timesup.png       (200x112)
    night-player.png  (250x164)
    night-enemy.png   (proportional)
    night-sports.png  (proportional)
    night-taxi.png    (proportional)
    night-sky.png     (640x216, Atlanta skyline)
    crash.mp3
    pass.mp3
    sports-pass.mp3
    taxi-pass.mp3
    lap.mp3
    offroad.mp3
    music.mp3
    night-music.mp3
    gameover.mp3
    win.mp3
```

---

## Links

- [Story and Instructions](story.html)
- [Check Out the Band's Promo Reel](https://www.youtube.com/watch?v=P-OnPcTdzCw)
- [cantdrive55atl.com](https://cantdrive55atl.com/)

## Credits

Concept, design, art direction, story, and audio: [Andrew Doss](https://www.andrewdoss.com/)

Guitar on music and sound effects: [Stephen Gendron](https://www.instagram.com/stephengendronmusic)

Game engine and code: Built with Kiro AI-assisted development

Inspired by Sammy Hagar's "I Can't Drive 55" and the Atlanta tribute band Can't Drive 55.

© 2026 Andrew Doss. All Rights Reserved.
