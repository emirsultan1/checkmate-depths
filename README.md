# Checkmate Depths

A mobile chess puzzle game where players descend through themed dungeons, solving puzzles that get harder the deeper they go.

> 🚧 **Status:** In active development. Target: first release on the App Store and Google Play.

## How It Works

- The game is split into **dungeons**, each with **10 chess puzzles**.
- Every dungeon draws from a higher difficulty band, starting easy and ending with puzzles that challenge strong players.
- Players get **3 lives per dungeon**. A wrong move costs a life.
- Lose all 3 lives and the dungeon is **locked for a cooldown period**. On retry, the player gets a fresh set of puzzles from the same difficulty band.
- Clearing a dungeon unlocks the next one, each with its own theme and background.
- A **global leaderboard** ranks players by how deep they have gone.

| Dungeon | Theme | Puzzle Rating |
|---|---|---|
| 1 | Crypt | 400–800 |
| 2 | Catacombs | 800–1100 |
| 3 | Flooded Halls | 1100–1400 |
| 4 | Lava Depths | 1400–1700 |
| 5 | Dragon's Lair | 1700–2000+ |

## Tech Stack

**Mobile app**
- Flutter (Dart), for iOS and Android from a single codebase

**Backend**
- Java 21, Spring Boot 3
- PostgreSQL
- Spring Data JPA
- Flyway for database migrations

## Architecture

The backend is the source of truth for all game state. The mobile app only displays puzzles and sends moves.

- **Puzzle selection:** the server chooses each puzzle from the correct difficulty band, so the client never knows the solution in advance.
- **Move validation:** every move is checked on the server.
- **Lives and cooldowns:** tracked and enforced server-side, so they cannot be bypassed by changing the device clock.
- **Puzzle import:** a one-time import job loads puzzles from the Lichess puzzle database, keeping only puzzles with reliable ratings (low rating deviation, high play count, high popularity) and assigning them to dungeons by rating.

## Project Structure

```
.
├── backend/   # Spring Boot API
└── mobile/    # Flutter app
```

## Getting Started

### Backend

```bash
cd backend
./mvnw spring-boot:run
```

### Mobile

```bash
cd mobile
flutter pub get
flutter run
```

Run on the iOS Simulator (Xcode) or the Android Emulator (Android Studio). No physical device needed for development.

## Roadmap

- [ ] Backend: puzzle import job and database schema
- [ ] Backend: dungeon, lives, cooldown, and leaderboard endpoints
- [ ] Mobile: chessboard and puzzle screen
- [ ] Mobile: dungeon map, results, and leaderboard screens
- [ ] Deploy backend
- [ ] Release on the App Store and Google Play

**Planned for later:** daily challenge, hints, more dungeons, push notifications.

## Credits

Chess puzzles come from the [Lichess puzzle database](https://database.lichess.org/#puzzles), released into the public domain. Thank you to Lichess and its community.

## Author

**Emir Sultan**
[GitHub](https://github.com/emirsultan1) · [LinkedIn](https://linkedin.com/in/emir-sultan)
