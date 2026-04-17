# Weather or Not

Weather or Not is a Flutter mobile app that helps users decide what to wear by generating weather-aware outfit suggestions from their own wardrobe.

Instead of making clothing decisions from scratch every morning, users can store wardrobe items, set personal temperature comfort preferences, and get outfit recommendations tailored to both weather conditions and planned activities.

## Why This App Exists

Daily outfit selection is a small but recurring problem:

- It consumes time when people are in a rush.
- It is easy to underdress or overdress when weather changes quickly.
- Plans for the day (commute, casual meeting, outdoor activity) are often ignored.

Weather or Not solves this by combining personal wardrobe data, forecast data, and activity context into a practical recommendation engine.

## Core Features

- Weather-based outfit recommendations from a personal wardrobe
- Personalized temperature comfort thresholds (cold/warm perception)
- Wardrobe management: add, edit, delete, search, and favorite items
- Clothing metadata support: categories, subcategories, attributes, style tags, formality, colors
- Monthly planner with activities that influence recommendations
- Saved outfits for quick reuse
- In-wash item status to temporarily exclude clothes
- Reroll/refresh suggestions for more variety
- Location picker with current-location support and weather-station fallback logic

## How Recommendations Are Generated

The suggestion engine uses a point-based scoring approach with hard constraints:

1. Filter candidates by hard weather boundaries (temperature, rain, wind).
2. Score remaining items by activity fit, formality, style compatibility, and color harmony.
3. Respect practical constraints such as commuting and daily context.
4. Inject controlled randomness to avoid repeating the exact same outfit too often.

This creates suggestions that are both sensible and varied.

## Technical Highlights

- Built with Flutter and Dart using provider-based state management
- Integrates weather data via DWD-related endpoints and station metadata
- Handles real-world API inconsistency with fallback station search by radius
- Uses interpolation logic to estimate "live" conditions when stations are incomplete
- Persists user preferences, wardrobe data, and planner information locally

## Engineering Challenges And Solutions

- Incomplete weather station data:
  Introduced nearest-station fallback and weather interpolation strategies to keep recommendations available.

- Planner and home-screen synchronization issues:
  Refined state flow and update triggers so planned activities reliably affect daily suggestions.

- Repetitive outfit outputs:
  Added controlled randomness to increase diversity while preserving relevance.

- Activities not influencing suggestions strongly enough:
  Rebalanced algorithm weighting and constraints so activities materially change outcomes.

- Temperature mismatches (e.g., heavy layers when warm):
  Added stricter weather constraints to prevent impractical recommendations.

- UI complexity in selection dialogs:
  Improved information architecture with grouping and search for faster item/activity selection.

- State race conditions causing instability:
  Improved provider update ordering and defensive checks to prevent crashes and inconsistent state.

## Tech Stack

- Framework: Flutter
- Language: Dart
- State management: provider
- Networking: http
- Local persistence: shared_preferences, file storage via path_provider
- Device capabilities: geolocator, image_picker
- Date and planning UI: intl, table_calendar

## Project Structure

The codebase is organized by responsibility:

- `lib/models`: Domain models for weather, outfits, wardrobe items, planner entries
- `lib/services`: Weather integration, storage, planner logic, outfit generation
- `lib/providers`: App-level state orchestration
- `lib/screens`: User-facing screens (home, wardrobe, planner, settings, details)
- `lib/widgets`: Reusable UI components

## Getting Started

### Prerequisites

- Flutter SDK (stable channel)
- Dart SDK (installed with Flutter)
- Android Studio or Xcode for device/emulator builds

### Run Locally

```bash
flutter pub get
flutter run
```

## Current Status

The app is functionally complete and demonstrates:

- End-to-end weather-aware recommendation logic
- Robust handling of imperfect external weather data
- Practical wardrobe and planner workflows for day-to-day use

## Future Improvements

- Cloud sync for wardrobe and planner data
- Better explainability for recommendations ("why this outfit")
- Expanded style intelligence with stronger personalization over time
- Push notifications for significant weather changes
