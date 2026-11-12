# Sarkless Kitty Story Walk

An offline-first, location-triggered audio storytelling app for a Story Walk in Farndale, North York Moors, developed for [3-Minute Arts CIC](https://example.org).

The first story is *Kitty: A Farndale Ghost Story*. As walkers follow a designated route, the app plays sections of the story at set locations, using narration, character voices, music and sound effects. At selected points, walkers may make a choice that changes what they hear next.

> **Status:** Early planning. The repository currently contains only three sample audio files (MP3, 128 kbps) that will be used to build the first prototype. Development of the full app is planned for 2027–28, subject to funding.

---

## Aims

- Make the story feel as though it unfolds around the walker as they move through the landscape.
- Work reliably in rural areas with patchy or no mobile reception.

- Keep story content separate from application code, so the app can later be reused for other Story Walks (North York Moors, coast and Cleveland) without being rebuilt.

## Design principles

1.  All story content is downloaded or bundled in advance. GPS triggering and audio playback must work with mobile data and Wi-Fi switched off.
2. GPS accuracy varies, especially near trees, buildings and uneven ground. A manual "play this section" option is always available. QR codes at story points may be considered later, if incorporated into physical trail signage.
3. Story structure, locations and audio references live in a structured file, not in the app source.
---

## Sample audio

The three MP3 files are sample narration mixed with ambient sound effects. They are placeholders for testing playback and location association, and will eventually be replaced by recordings with actor voices and richer soundscapes.



 The final app should be able to handle ambient sound independently of speech (volume and duration).

---

## Planned features

### Location-based playback
- Simple map or route display showing the walk and its story locations
- GPS detection of approach to a designated point, with a configurable trigger radius
- Automatic playback of the relevant section, with a clear indication of the current story location
- Clear notification when a new section becomes available

### Audio and interactivity
- Playback of narration, character voices, music and sound effects
- Independent handling of ambient sound and spoken audio
- Pause, resume, replay and volume controls
- Simple choices or prompts at selected points, leading to different story paths

### Offline operation
- Download the complete story and audio before the walk
- Local storage of all content on the phone
- Check that content is available before the walk begins

### Usability and recovery
- Clear instructions for starting the walk and downloading the story
- Manual start and replay of any section
- Ability to return to previous sections if a location is missed

---

## Proposed architecture

| Component | Approach |
|---|---|
| Mobile app | Flutter (Dart), allowing Android and iOS from one codebase. The prototype may target a single platform first. |
| Location service | Flutter GPS package such as `geolocator`. Stores each location's lat/long, checks position periodically, calculates distance to the next story point and triggers when the walker enters its radius. |
| Audio playback | `just_audio` or a comparable Flutter package. Plays local files, supports narration, dialogue, music and effects, and manages transitions between sections. |
| Story structure | JSON, stored separately from app code (see below). |
| Offline storage | Prototype: audio and story data bundled in the app. Later: downloadable story packages stored locally. |

### Story data format

Each story section would contain:

- A unique identifier
- The location or trigger associated with it
- The audio file to play
- Any accompanying text or instructions
- Optional choices, with the identifiers of the next sections

A simple branching structure is sufficient initially. A sophisticated narrative engine is not needed.


### System flow

1. The user opens or downloads the story.
2. The app loads the route and its story locations.
3. The user starts the walk.
4. The app checks the phone's GPS position.
5. On reaching a designated location, the matching audio section plays.
6. The user listens and, where offered, responds to a prompt or makes a choice.
7. The app selects the next section and continues as the walk progresses.

If GPS triggering fails, the user selects the section manually.

---

## Roadmap

### Stage 0: Proof of concept (current focus)
A small demonstration using the existing sample audio, ahead of any funding decision.

- [ ] Set up Flutter project and repository structure
- [ ] Add the three sample MP3s as bundled assets
- [ ] Basic UI: list of three stations with manual play, pause and replay
- [ ] Define three GPS locations (simulated locations are fine at this stage)
- [ ] Trigger the correct audio when the device enters a location's radius
- [ ] Show a clear "new section available" indicator
- [ ] Handle ambient sound separately from narration, if separate tracks are available

**Output:** a working demonstration of location-triggered audio with a manual fallback.

### Stage 1: Requirements and story mapping
- [ ] Agree the walking route and principal story locations
- [ ] Agree the sequence of story sections with the creative team
- [ ] Identify where audio triggers and interactive choices occur
- [ ] Confirm minimum features for the prototype

**Output:** route map, story flow diagram, finalised technical specification.

### Stage 2: Basic application prototype
- [ ] Route and story location display
- [ ] Real GPS detection with configurable trigger radius
- [ ] Audio playback of sample recordings
- [ ] Manual controls to select and replay sections

**Output:** working demonstration of location-triggered audio playback.

### Stage 3: Interactive and offline functionality
- [ ] Move story structure into JSON, separate from app code
- [ ] Add at least one interactive choice with branching
- [ ] Store audio and story data locally
- [ ] Test with mobile data and Wi-Fi switched off
- [ ] Basic error handling and recovery

**Output:** working prototype of the interactive, offline audio experience.

### Stage 4: Field testing and refinement
- [ ] Test along the actual Farndale route
- [ ] Check GPS accuracy and trigger reliability, especially in wooded areas
- [ ] Tune trigger distances and timing
- [ ] Test playback, battery consumption and usability
- [ ] Gather feedback from a small group of walkers

**Output:** a tested prototype suitable for demonstration and further development.

### Stage 5: Towards a final product
Subject to prototype success and further funding:

- [ ] Polished version for public use
- [ ] Downloadable story packages and support for additional Story Walks
- [ ] Straightforward content-management process for community groups
- [ ] Improved accessibility, plus additional language or text options if needed
- [ ] Optional QR code access at physical story points
- [ ] Distribution through app stores

---

## Prototype scope

A successful prototype will demonstrate:

- A short section of the Farndale route
- At least three GPS-triggered story locations
- Recorded audio and sound effects
- At least one interactive choice
- Offline playback
- Manual controls as a fallback

## Technical risks and mitigations

| Risk | Approach |
|---|---|
| Poor mobile reception | Download all content in advance; operate offline |
| Inaccurate GPS | Manual selection and replay of sections; configurable radius tested on the route |
| Battery consumption | Avoid overly frequent GPS checks; test on the route |
| Different phone models | Test on a small range of Android and iOS devices |
| Walkers moving at different speeds | Trigger by location, not timing |
| Missed story locations | Allow users to return to previous sections |
| Changing story content | Keep story data separate from application code |

## Longer-term vision

A reusable platform for community-led Story Walks. The underlying app stays largely the same, while routes, locations, recordings and story structures are supplied as separate content packages. Local groups could then develop their own walks based on local folklore, history, landscape and personal stories without commissioning a new app each time.

---
