# Catapult Tracker

**Created by Bachar Mourched. © 2026, all rights reserved.** See [LICENSE](LICENSE). Open the app at https://bacharmourched-droid.github.io/Catapult/.

A live projectile tracker for the catapult competition. It follows a brightly coloured ball through a
camera feed, draws its trajectory over the video, and shows the range **R** and the launch speed
**v₀ = √(R·g)** (45° launch) in large type for a projector. It also shows the flight time and maximum height.

It is a single file, `index.html`, with no install, no libraries and no internet connection needed.
Open it in Chrome or Edge on the laptop that drives the projector.

> The numbers are a live readout for the audience. The official score is still the tape measure.

---

## Opening the page

* **Easiest:** double-click `index.html`. Chrome and Edge allow the camera on `file://` pages.
* **If the camera is blocked** (some browsers or IT policies), serve the folder locally and open the localhost URL:
  ```bash
  cd projectile-tracker
  python3 -m http.server 8000      # then open http://localhost:8000
  ```
  You can also host it as a static page (e.g. GitHub Pages). Camera access needs `https://` or `localhost`.

The **⚙ Setup** drawer opens on the left. Close it (press `S`) for the audience view.

| Key | Action |
|---|---|
| `Space` / `N` | Next launch: clear the trail and re-arm |
| `S` | Show/hide setup |
| `F` | Fullscreen |
| `M` | Show the detection mask (magenta) |
| `C` | Calibrate (2 clicks) |
| `P` | Pick the ball colour (1 click) |
| `Esc` | Cancel a click mode |
| Click on the video | Lock the tracker onto the object you clicked |

---

## Student tutorial video

[`tutorial.mp4`](tutorial.mp4) is a 2-minute video with voice-over and captions for the students. It
covers the setup, where to stand, waiting for **READY**, launching, reading the results, and the next team.
Show it before the competition, or loop it on a second screen. It is also linked at the top of the app's
⚙ Setup panel. 

## Rehearse at your desk (10 minutes)

### 1. Demo mode: no camera, no ball

Setup → **🧪 Demo (simulated)** plays a synthetic side view of a catapult throwing an orange ball at 45°.
It goes through the same tracking code as the camera.

1. Click **Calibrate**, then click the **0 m** mark and the **5 m** mark on the white line.
   Real length = `5`. (Or press **Auto-calibrate demo**.)
2. Watch a launch. The status pill goes **READY → IN FLIGHT → LANDED**, the trail is drawn, and the
   dashed parabola, range bar and **R = … m** label appear.
3. Compare the results with the **DEMO truth** banner in the top-left corner of the video:
   * With *Range measured to = ground*, **R** should match the **ground range**.
   * With *Range measured to = launch height*, **R** should match the **same-height range**,
     and **v₀** should match the true **v₀**.
   In testing, R matched the truth to about 1 cm and v₀ to about 0.01 m/s.
4. Press `Space` for the next launch, or set *Auto next launch* to 5 s and let it run.
5. Set *Demo* to **realistic** to practise under event-day conditions: camera noise, passing clouds,
   motion blur, a smaller ball, and orange things that are not the ball. These are a spectator's shirt,
   a cone, and someone walking past. Try the mask, the detection zone and clicking the ball.

### 2. A recorded video of your own setup

This is the best rehearsal. Record a few throws with a phone, or with the actual webcam, from the
camera position you plan to use. Then Setup → **🎞 Video file**.

* Calibrate on the tape that is visible in the clip, pick the ball colour, and play the clip.
  **Restart** replays it. **Speed** slows playback without affecting the physics, because the app
  uses the video's own timestamps.
* **Slow-mo clips:** set *Slow-mo factor* to the ratio of capture fps to playback fps
  (for example 240 → 30 gives 8). Otherwise the flight time is reported as 8× too long.
  Range and v₀ do not depend on timing, so they are correct either way.

### 3. Live webcam with a ball in your hand

Setup → **📷 Camera**, then pick the camera from the list. External USB webcams appear there too.

* Click **Pick colour**, then click on the ball. Turn **Show mask** on: only the ball should be magenta.
* Hold the ball still for about half a second (until **READY**), then toss it in an arc across the frame.
  It should be tracked, and the trail should end where it lands.

---

## Using a phone as the camera

* Open the page over `https://` (for example the GitHub Pages link), then tap **⚙ → 📷 Camera** and allow access.
* **Hold the phone sideways (landscape).** In portrait, the horizontal view is much narrower. The app reminds you.
* If the phone reports a zoom range, a **Zoom** slider appears, and the app starts at the widest setting.
  Phones with several rear lenses list each one under **Camera**. An ultra-wide lens fits more in, but
  bends straight lines near the edges, so keep the flight and the reference line away from the edges.
* Put the phone on a **tripod**. Rotating or moving it after calibration invalidates the calibration.
  If the picture changes shape, the app notices and asks you to calibrate again.
* The screen is kept awake while a source is running, where the browser allows it.
* **Outdoors:** after picking the ball colour, tap **🔒 Lock exposure & colour** if your camera offers it.
  This stops automatic exposure and white balance from shifting the ball's colour as clouds pass.
  **Brightness** adjusts exposure compensation. Both appear only on cameras that support them, mostly
  Android Chrome.
* On a slow device, the app lowers the *Processing width* by itself if detection can't keep up, and tells you.

## Event day: setup at the field

**Camera placement**
* Put the camera side-on to the flight: its view should be perpendicular to the throwing direction,
  about 10 m away, roughly level, on a tripod. **The camera must not move after calibration.**
* Frame everything from the catapult to beyond the longest expected landing spot, with some sky above
  the highest point (at 45°, the peak height is about R/4).
* *Camera mode* defaults to **Widest view (30 fps)**. *Smooth (60 fps)* tracks fast balls better, but many
  phones crop the picture in 60 fps mode. Only switch if the view stays wide enough. The actual fps and
  resolution are shown at the bottom of the results panel.

**Reference line (calibration)**
1. Lay a tape measure or chalk line **on the ground along the throwing direction**, in the same vertical
   plane as the flight, starting at the catapult (e.g. 0 m to 5 m, or longer if you can).
2. Setup → *Real length* = that distance → **📏 Calibrate**, then click the two ends of the line.
   The cyan line also defines **horizontal** (tilt is corrected) and **ground level**.
3. Check the scale in the info line, e.g. "140 px/m (7 mm per pixel)".
   A longer reference line gives better accuracy.

**Ball colour**
1. Place the ball in the catapult cup, then **🎨 Pick colour** → click on the ball.
2. Turn on **Show mask (M)**. The ball should be a solid magenta dot and nothing else should be magenta.
   * Background lights up (brown wood, orange shirts, cones, autumn leaves): raise *Saturation min*
     and *Brightness min*, narrow the hue range, or use **▭ Detection zone** to draw a box around
     the flight area.
   * Ball flickers or disappears in flight: lower *Saturation min* and *Brightness min*, or lower *Min blob*.
3. The tracker picks the most *ball-like* orange object. That means round, the size of the previous
   ball, and close to where the previous ball sat in the cup, not simply the biggest one. So shirts,
   cones and faces are normally ignored. If the green **lock ring** is still on the wrong object,
   **click on the ball** to lock onto it.
4. Re-pick the colour whenever the light changes (clouds, sunset). This takes 5 seconds.

**Dry run.** Do one or two practice throws and compare R with the tape before the competition starts.

**During the competition**
1. Type the team name in the results panel. It appears in the header and in the launch log.
2. Wait for **READY — BALL LOCKED** (green), then launch. The ball must sit still in the cup for a
   moment first. Until it does, the status shows *BALL SEEN — HOLD STILL* and motion is ignored.
3. Results appear when the ball lands. Press **Space** before the next team.
4. **CSV** downloads the launch log. The log, calibration and colour settings are saved in the browser
   and survive a page reload.

---

## How it works

1. **Detection.** Each frame is shrunk to the *processing width* (default 640 px) and every pixel is
   tested against the HSV thresholds. Connected pixels are grouped into blobs, and blobs outside the size
   limits are dropped. This takes about 10 ms per frame, with no ML.
2. **State machine.**
   * **ARMED**: follow the locked blob. When it moves faster than the *launch trigger* (percentage of
     frame width per 1/30 s) **straight from rest**, the flight starts. The place where it was sitting
     still (in the cup) becomes the **launch point**. Motion that doesn't start from rest is ignored,
     for example when the tracker is re-armed while a ball is still in the air.
   * **IN FLIGHT**: each frame, the app predicts where the ball should be (last velocity plus gravity)
     and takes the closest blob within a gate. This keeps it from jumping to other orange objects.
     The flight ends when the ball reaches the ground line, stops moving, or is lost. Short dropouts,
     up to 0.8 s while the ball should still be airborne and in frame, are bridged.
   * **LANDED**: shows the results until *Next launch*.
3. **Physics.** The tracked points are converted to metres using the calibration line (x along the line,
   y perpendicular to it, upward). A parabola y(x) is fitted, with one round of outlier rejection, for
   example to remove points from the catapult arm. From the fit:
   * **R** = horizontal distance from the launch point to where the parabola meets the landing level,
     the ground line by default. Because R comes from the fit, it is still correct when the ball lands
     slightly out of frame or behind something.
   * **v₀ = √(R·g)**, the 45° same-height formula.
   * **Flight time** = R / horizontal speed, where the horizontal speed comes from a linear fit of x(t).
   * **Max height** = the vertex of the parabola above the landing level.
   * The small line under the numbers shows **cross-checks**: v₀ and angle measured directly from the
     tracked path, and **g** recovered from the curvature. If the fitted g is far from 9.8, the
     calibration (or the slow-mo factor) is probably wrong.
4. If a "flight" is not a downward-opening parabola, for example someone carrying the ball past the
   camera, it is ignored and the tracker re-arms by itself.

### One physics caveat to share with the audience

v₀ = √(R·g) assumes the ball **lands at the height it was launched from**. A catapult releases the ball
somewhat above the ground, so the ground range is a little longer, and √(R_ground·g) **overestimates**
v₀ by a few percent. For a 0.6 m release height and v₀ ≈ 9 m/s, it is about 3%.
* *Range measured to = ground (calibration line)*: matches what the tape measures. This is the default.
* *Range measured to = launch height*: uses the same parabola, cut at the release height. This gives
  the R that makes √(R·g) exact.
The "tracked launch" speed shown under the numbers does not depend on this choice.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| Status says **CALIBRATE FIRST ▸** | Tap it, then tap both ends of your reference line. |
| "NO BALL DETECTED" with the ball in view | Pick colour again; lower *Saturation min* / *Brightness min*; check *Min blob*. |
| Lock ring on the wrong object | Click on the ball; use a detection zone; tighten the colour sliders (check with the mask). |
| Launch not detected | Lower the *Launch trigger*. A higher trigger means fewer false starts from people walking around. |
| "Ball lost mid-flight — no result" | The ball vanished in the air before the app had enough of the arc to extend it to the ground. It shows no number rather than a wrong one. Check the mask during a throw: motion blur fades the colour, so lower *Saturation min*. You can also raise *End if lost for*. |
| Flight ends too early | Raise *End if lost for*; check the mask during a throw (motion blur fades the colour). |
| R clearly wrong | Recalibrate; make sure the reference line is on the ground, along the throw, and in the same plane as the flight; check the camera has not moved. |
| Low fps | Lower the *Processing width* to 480. Close other apps. |
| Ball too small to detect (a few pixels) | Raise the processing width to 960/1280, use a larger ball, or move or zoom the camera closer. |
| Camera permission error | Serve the page from `http://localhost` (see above), or allow the camera in the browser's site settings. |

Tips for robust outdoor tracking: use a **large, matte, fluorescent ball** (orange, yellow or pink),
keep the sun **behind the camera**, avoid a background of the same colour, and set the camera to
a fixed exposure if possible, because auto-exposure "pumping" changes the colour.
