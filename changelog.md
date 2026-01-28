# Changelog  (28/01/2026)
All notable changes to **Sublime Sounds – Rhythm Master** will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)  
and this project follows a rolling release model during beta.

---

## [Unreleased]
### In Progress
- Mobile MetaMask in-app browser refinements (media start restrictions)
- Polygon NFT pool expansion
- Cross-chain UI polish

---

## [v0.9.0] – Polygon Expansion Update
**Major multi-chain release**

### ✨ Added
- **Polygon support (full gameplay integration)**
  - MetaMask login
  - Polygon wallet session handling
  - Polygon-specific score submission (`submit-score-polygon`)
  - Polygon leaderboard entries alongside WAX scores
- **wSSN rewards on Polygon**
  - ERC-20 wSSN settlement via `settle-wssn`
  - One payout per run (restarts forfeit rewards)
  - Replay protection using `run_id`
- **Polygon NFT gameplay support**
  - Bridged NFTs playable in Rhythm Master
  - Polygon NFT metadata normalization (image / audio)
  - Chain-aware NFT source handling
- **Polygon NFT drops**
  - On-hit NFT reward logic
  - `transfer-polygon-nft` Edge Function
  - Polygon NFT pool backed by database (no minting on Polygon)
- **Chain-aware UI**
  - “Polygon NFT received” badge
  - Polygonscan links for NFT receipts
  - wSSN label replaces SSN on Polygon
  - Mixed-chain leaderboard support

### 🎮 Gameplay
- Polygon and WAX now share a unified, stable game engine
- NFT selection works identically across chains
- Track media preloads correctly on both chains
- Audio-only NFTs display artwork during gameplay
- Video NFTs play video only on start (no image bleed)

### 🧠 Media System (Major Refactor)
- **Strict media exclusivity enforced**
  - Audio *or* video, never both
- **Clear lifecycle separation**
  - `applyTrackVisuals()` → idle preview only
  - `startGame()` → playback only
  - `endGame()` → full cleanup
- **Idle preview behaviour**
  - NFT image always shown on selection (audio *and* video NFTs)
- **Playback behaviour**
  - Video NFTs hide image and play video
  - Audio NFTs retain image and play audio
- Eliminated:
  - Double media playback
  - Ghost audio/video on tab switch
  - Media restarting on visibility change
  - Autoplay regressions on mobile

### 🏆 Leaderboards
- Multi-chain competition support
- WAX and Polygon scores shown together
- Chain-safe user identifiers
- Ready for address truncation display on Polygon

### 🔐 Security & Integrity
- Replay-safe reward settlement
- One NFT / reward per run enforcement
- Chain-specific backend paths (no cross-contamination)
- No silent auto-bridging

---

## [v0.8.x] – Stability & Upgrade Foundations
### Added
- Stable NFT upgrade flow (Levels 1–4)
- SSN upgrade payment tracking
- Leaderboard season support
- Track-based leaderboard filtering

### Fixed
- Leaderboard score mismatches
- NFT scan performance issues
- Upgrade path validation bugs
- Audio/video preload edge cases

---

## [v0.7.x] – Core Gameplay Beta
### Added
- Rhythm gameplay engine
- Combo, multiplier, and reward notes
- SSN earning through gameplay
- NFT-based track selection
- Background image / media support
- WAX wallet login (Anchor & WCW)

---

## Notes
- Polygon is intentionally **parallel**, not a mirror of WAX
- WAX logic remains untouched and stable
- All new chain features are additive and isolated
- Rhythm Master remains free-to-play with no required payments

---

**Sublime Sounds – Rhythm Master**  
Multi-chain rhythm gameplay powered by music NFTs 🎵


# CHANGELOG.md (16/01/2026)
All notable changes to **Sublime Sounds – Rhythm Master** will be documented in this file.

This project is currently in active development and public beta testing.

---

## [Beta 2 – Stable Gameplay + Security Lockdown] - 2026-01-16

### ✅ Core Gameplay (Stable)
- Game runs reliably end-to-end with:
  - NFT selection
  - Track loading (image / audio / video)
  - Start flow
  - Falling notes + hit detection
  - Score + combo tracking
  - End game screen + reset back to idle state

### ✅ Media System Fixes (Audio + Video)
- Fixed **video replay / 2nd play issues** by hard-resetting video element safely per run.
- Video now **preloads without autoplay** (does not start playing just by selecting an NFT).
- Restored stable **audio playback** for audio-only NFTs.
- Fixed media state cleanup so the next run starts cleanly.

### ✅ Restart System (Working)
- Restart now works correctly for:
  - Audio-only NFTs
  - Video NFTs
- Game properly ends on media end events (audio-ended / video-ended).
- Restart no longer causes endless falling notes or stuck gameplay state.
- Restart respects:
  - `paidForThisTrack`
  - `MAX_RESTARTS` (non-admin users)
  - `ADMINS` bypass rules
- Added safer restart logic to avoid locking the game loop.

### ✅ Logout Cleanup (Fixed)
- Logout now performs a full hard stop of gameplay state.
- Media elements are cleared correctly so no audio/video remains visible/playing after logout.

### ✅ UI Improvements / Quality of Life
- Login buttons now hide after successful authentication:
  - Anchor login button hidden after login
  - WAX login button hidden after login
- Upgrade dropdown/UI now disables during gameplay (prevents changing upgrade options mid-run).
- Improved overall “idle → paid → start” flow stability.

### 🎨 Visual Enhancements (Arcade Neon Notes)
- Notes updated to a more arcade / neon “bloom” style:
  - Solid colored note bodies
  - Neon glow around notes
  - Improved readability + punch
- SSN notes color adjusted (now blue as requested).
- Hitline glow added for better visual feedback.

### 🔒 Security Hardening (CRITICAL)
- Full Supabase security lockdown completed:
  - **RLS enabled on all tables**
  - Direct table writes blocked from public clients
  - Only Edge Functions using Service Role can write where required
- Confirmed game remains functional after lockdown:
  - Auth-session still works
  - Wallet scan still works
  - NFT loading still works
  - Score submit still works

---

## 🚧 Known Issues / Not Included Yet

### ❌ Upgrades (Disabled for Beta 2)
Upgrades are not yet released in Beta 2 because they must be restored exactly to the required ruleset:

- Level 1 → 2 = **4000 SSN** and requires **BURN + MINT**
- Level 2 → 3 and 3 → 4 = SSN payment (if required) + Atomic mutable update
- No skipped levels, max level = 4
- SSN txids must be tracked in `ssn_upgrade_payments` (no reuse)

---

## 🎯 Next Planned Work
- Restore full NFT upgrade system with strict rule enforcement:
  - Frontend user-signed burn + mint for Level 1 upgrade
  - Backend finalizes DB + atomic mutable updates for Level 2+
- Final pass on upgrade UI/UX once upgrade logic is confirmed stable.
- Prepare **Final Beta Test** release once upgrades are fully working.

---


# Changelog (15/01/2026)

All notable changes to **Sublime Sounds – Rhythm Master** will be documented in this file.

---

## [Unreleased] – 2026-01-15
### ✅ Stable / Working (Core Gameplay + Wallet + Media + Leaderboards)

#### 🔐 Wallet Login + Session Auth
- Anchor login working correctly
- `auth-session` returns a valid JWT and is stored in `window.sessionToken`
- Auto wallet scan runs after login
- NFT list loads from Supabase DB successfully (`fetch-wallet-nfts`)
- Logout works and resets game state cleanly

#### 🎮 Gameplay Flow
- Game starts reliably after **paying 100 SSN** and clicking Start
- Paid play gating is enforced correctly (no free play unless admin/dev logic allows)
- Restart flow works correctly after game end
- Restart attempts are tracked + limited (non-admin users)
- Restart no longer causes broken states / stuck runs

#### 🎥 Video / 🔊 Audio Media System
- Track media now preloads safely without autoplay on selection
- Video NFTs no longer auto-play immediately when selected (only plays after Start)
- Video replay / second play is stable (hard reset + safe reload)
- Audio playback is stable again (including autoplay mute/unmute handling)
- Video end triggers `forceEndGame("video-ended")` correctly
- Audio end triggers `forceEndGame("audio-ended")` correctly
- Media loading UI works (`showMediaLoading()` / `hideMediaLoading()`)

#### 🧹 Hard Stop / Cleanup Improvements
- `hardStopGame(reason)` properly stops:
  - RAF loop
  - failsafe timer
  - media playback (audio + video)
  - notes + visual effects
- Special handling added:
  - Restart uses `ended=false` so next run starts cleanly
  - Logout performs full media wipe (removes `src`, calls `.load()`, hides video, clears background)

#### 🏆 Leaderboards
- Score submission is working again via Supabase RPC:
  - `submit_leaderboard_score`
- Payload includes correct fields:
  - season
  - template_id
  - wallet (from JWT)
  - score
  - max_combo
  - track_name (nullable)
- Leaderboard loads per-template correctly (no longer shows previous template results)

#### 🔒 UI Locking During Runs
- Upgrade UI (dropdown + upgrade button) now locks during gameplay
- Upgrade UI unlocks after run end / reset

#### 🧾 SSN Settlement (Front-End Flow)
- Settlement call is correctly gated:
  - not called on restart run
  - requires `sessionToken`, `user`, `currentTrack`, and `ssnEarnedThisRun > 0`
- Settlement errors are caught and logged without breaking gameplay
- Current error is CPU throttling / failure-limit on chain (external WAX CPU condition)

#### 🧼 Login Button UX
- WAX + Anchor login buttons are hidden after login
- Buttons return on logout

---

### ⚠️ Known Issues / Not Yet Working

#### 🧬 NFT Upgrades (Main Remaining Issue)
- Upgrade system is still incomplete / unstable
- Upgrade dropdown and upgrade flow still needs final fix + validation
- Priority is restoring the exact previous upgrade behaviour:
  - Level-based upgrades (L1→L2, L2→L3, L3→L4)
  - Correct SSN costs per level
  - No skipped levels
  - Stable frontend ↔ backend interaction
  - Uses `upgrade-nft` Supabase Edge Function as the upgrade authority

---

## Notes
- Current build in use: `rythummasterold.html`
- Wallet user tested: `a1hd.wam`
- Supabase Edge Functions confirmed active:
  - `auth-session`
  - `fetch-wallet-nfts`
  - `submit-score`
  - `settle-ssn` (currently failing due to CPU usage limits on WAX push_transaction)

---


# Changelog (10/10/26)

All notable changes to the Rhythm Master NFT Upgrade & SSN system will be documented in this file.

## [Unreleased]
- Preparation for new NFT drops
- Final verification of SSN settlement edge cases

---

## [2026-01-09] – NFT Upgrade System Stabilisation

### ✅ Fixed
- **Critical bug:** `txid is not defined`
  - Root cause was a leftover debug `console.log` referencing `txid` instead of `ssn_txid`
  - This caused false error popups even when upgrades succeeded
- **Upgrade skipping levels**
  - Enforced strict upgrade progression:
    - Level 1 → Level 2
    - Level 2 → Level 3
    - Level 3 → Level 4
  - Backend now validates `expectedToLevel = currentLevel + 1`
- **Invalid upgrade paths**
  - Backend now rejects any path where `to_level` does not match the expected next level
- **Level 1 auto-upgrade regression**
  - Restored correct handling of `upgrade_path = "auto"` for Level 1
  - Locked Level 1 upgrades to template-based paths only

### 🧠 Improved
- Upgrade path resolution is now **deterministic**
  - Uses `(from_level → to_level)` instead of trusting client input
- SSN cost validation hardened
  - Backend now throws if `ssn_cost` is missing or invalid
- SSN upgrade payments made idempotent
  - Duplicate `ssn_txid` reuse is blocked
- Wallet NFT level normalization fixed (no more `|| 1` bugs)
- Client upgrade UI now mirrors backend rules exactly

### 🔒 Security
- Upgrade paths can no longer:
  - Skip levels
  - Jump multiple levels
  - Be forged by client manipulation
- SSN payment records are validated and locked before upgrades apply

### 🧪 Verified Working
- Level 1 → Level 2 (burn + mint)
- Level 2 → Level 3 (atomic update)
- Level 3 → Level 4 (atomic update)
- SSN payments recorded in `ssn_upgrade_payments`
- Upgrade UI state recovery
- Anchor + WAX wallet compatibility

---

## [2026-01-07] – Leaderboard & Wallet Scan Fixes

### Fixed
- Leaderboard not clearing when switching NFTs
- Wallet scans timing out on large inventories
- Session token loss after wallet popups

### Improved
- Wallet scan UX
- Leaderboard reload logic per template + season


# Changelog (08/01/26)

All notable changes to this project will be documented in this file.

This project follows a pragmatic, production-focused development approach rather than strict semantic versioning.

---

## [Unreleased]
### Planned
- Resource provider / CPU sponsorship for NFT burn & upgrade transactions
- Upgrade lock auto-release on failed on-chain burn
- Admin override tools for stuck upgrades
- Optional CPU preflight checks before upgrade
- Upgrade retry / resume support
- Upgrade activity audit log (backend)

---

## [0.9.0] – 2026-01-07
### 🎮 Gameplay & Core Engine
- Stabilised full game lifecycle (start → play → end → restart)
- Fixed note spawning and clearing logic on track end
- Notes now clear immediately when audio or video finishes
- Prevented duplicate animation frames and race conditions
- Improved restart reliability across multiple consecutive runs
- Added failsafe end-game protection for stalled media

### 🎥 Media Handling
- Rewritten `loadVideoWithFallback` with safe gateway rotation
- Added preload token invalidation to prevent stale media loads
- Fixed video/audio desync on restart
- Added robust fallback from video → audio on preload timeout
- Prevented media reuse bugs when switching tracks
- Improved autoplay handling for browser restrictions

### 🧠 State Management
- Hardened global game state flags (`playing`, `started`, `ended`)
- Added hard reset path for restart flow
- Prevented cross-track state bleed
- Improved tab visibility pause/resume handling
- Added guardrails to prevent double start or double end

### 🏆 Leaderboards
- Fixed leaderboard persistence bug when switching templates
- Corrected leaderboard reload logic per track
- Backend now enforces best-score-per-user-per-track
- Added explicit season and template scoping
- Improved leaderboard refresh timing post-submit

### 💰 SSN Economy
- Finalised SSN settlement flow via backend (`settle-ssn`)
- Ensured SSN boosts are applied authoritatively server-side
- Prevented duplicate SSN settlement on replay
- Improved error handling and non-blocking settlement logic

### 🖼️ UI & UX
- Improved upgrade overlay animations and feedback
- Added clear upgrade progress and completion messaging
- Fixed UI freezes caused by blocking async calls
- Improved mobile fullscreen handling and orientation unlock
- Disabled start button strictly based on payment state

---

## [0.8.0] – 2026-01-05
### 🔐 Authentication & Wallet
- Finalised Supabase JWT auth pattern for Edge Functions
- Fixed invalid session parsing and payload decoding
- Hardened auth checks across all backend endpoints
- Improved Anchor login resilience (cancel / retry safe)
- Standardised wallet actor resolution

### 🔥 NFT Upgrade System (Major)
- Implemented L1 → L2 upgrade flow with mandatory NFT burn
- Added backend upgrade locking (`nft_upgrade_locks`)
- Prevented concurrent upgrades on the same asset
- Ensured burn precheck happens before on-chain transaction
- Added retry-safe upgrade lock handling
- Integrated upgrade paths for higher-level NFTs
- Added frontend burn → upgrade sequencing

### ⛓️ On-Chain Integration
- Implemented `atomicassets::burnasset` via Anchor
- Correctly captured transaction IDs for upgrade validation
- Added explicit error handling for chain failures
- Properly surfaced CPU exhaustion errors to the UI
- Confirmed correct behaviour under CPU limits

> ⚠️ Note: NFT burns require WAX CPU.  
> Transactions may fail without sufficient CPU staking.  
> This is expected and handled gracefully.

---

## [0.7.0] – 2025-12-26
### 🧱 Backend Architecture
- Migrated core logic to Supabase Edge Functions
- Implemented `/scan-wallet-nfts` with database caching
- Added wallet ownership verification
- Introduced Firestore-compatible stubs for future expansion
- Added consistent CORS handling across all endpoints

### 🎵 NFT Track System
- Full dynamic track loading from AtomicAssets metadata
- Support for audio, video, and image-based tracks
- Dynamic background visuals per NFT
- Template-based track selection
- Added test-wallet free-play support

---

## [0.6.0] – 2025-12-12
### 🧪 Early Builds
- Initial rhythm engine (5-lane)
- Combo and accuracy tracking
- Basic scoring model
- Prototype leaderboards
- Early SSN token gating
- Initial WAX Cloud Wallet support

---

## Notes
- CPU exhaustion errors (`tx_cpu_usage_exceeded`) are not bugs.
- NFT burning on WAX is inherently CPU-expensive.
- Future releases will introduce sponsored CPU or fuel providers.

---


# Changelog

All notable changes to **Sublime Sounds – Rhythm Master** will be documented in this file.

The format is based on **Keep a Changelog**, and this project follows semantic-style versioning during beta.

---

## [Unreleased]

### Added
- NFT upgrade system (Level 1 → Level 4)
- On-chain NFT burn for Level 1 upgrades
- Backend upgrade locking to prevent duplicate or concurrent upgrades
- Visual NFT upgrade overlay and success animation
- NFT level badge displayed in UI
- NFT-specific score and SSN boost modifiers
- Retry logic for CPU-limit blockchain transactions
- Wallet re-scan button to refresh NFT state without reload
- Anchor wallet support alongside WAX Cloud Wallet

### Changed
- Refactored wallet handling to support both Anchor and WAX safely
- Unified transaction handling to prevent undefined RPC errors
- Improved NFT media loading with IPFS gateway fallbacks
- Improved game restart and session state handling
- Improved error messaging for failed upgrades and burns

### Fixed
- NFT selection not updating background / audio / video
- UI not reflecting selected NFT data
- False “Upgrade already in progress” errors
- Database schema mismatches for upgrade locks
- NFT lock rows not being cleared correctly
- Frontend crashes due to undefined wallet or RPC objects
- Burn transactions failing due to missing `asset_owner`
- Upgrade flow blocking gameplay incorrectly
- Multiple race conditions between burn, mint, and UI refresh

---

## [0.9.0-beta] – 2026-01-03

### Added
- NFT-based track selection
- Game score submission and leaderboard per track
- SSN token payments to start tracks
- NFT drops during gameplay
- Confetti and combo celebration effects
- Anchor wallet login
- Admin tools (clear leaderboard, season reset)

### Known Issues
- IPFS media may fail on some gateways (fallbacks applied)
- CPU-heavy accounts may temporarily hit WAX rate limits
- Mobile browser wallets may require external app handling

---

## [0.8.0-beta] – Initial Beta

### Added
- Core rhythm gameplay
- WAX Cloud Wallet login
- Score, combo, multiplier mechanics
- NFT-based audio tracks
- Basic leaderboard

---


# Changelog

## 📅 Date
**2025-12-21**

---

## 🎮 Rhythm Master (Game Client)

### Added
- **Accumulated SSN Tracking**
  - SSN earned during a run is now accumulated in real time.
  - SSN total is displayed at Game Over.
- **Wallet Re-scan Button**
  - Added “Re-scan Wallet” button to allow users to refresh NFT ownership without reconnecting.
  - Button correctly reuses existing NFT loading logic.
- **NFT Win UI**
  - NFT win badge added to Game Over screen.
  - Optional transaction link displayed when txid is returned.
- **Failsafe Game End**
  - Hard timeout to prevent stuck runs if audio/video fails.

### Fixed
- Game Over screen not appearing in some end states.
- Restart logic incorrectly consuming paid runs.
- Multiple NFT drop triggers per run (client-side safety flag added).
- Orientation pause/resume issues on mobile.
- Audio/video desync edge cases.

### Changed
- NFT drop logic now routed exclusively through `new-nft-drop` edge function.
- SSN payout logic deferred until end of run (no per-note transfers).
- Cleaner separation between **paid runs**, **free restarts**, and **admin bypass**.

---

## 🧠 NFT & Wallet Logic

### Added
- **NFT Pool System**
  - Introduced `nft_pool` table to manage claimable NFTs.
  - NFTs marked as claimed after successful transfer.
- **Server-Side NFT Eligibility**
  - Enforced:
    - Sublime-only hits
    - One NFT per user per season
    - Global cooldown
    - Probability-based drops

### Fixed
- NFT drops not triggering `send-nft` due to missing linkage.
- Invalid returns and misplaced logic in `new-nft-drop`.
- Missing JSON responses causing edge runtime crashes.

---

## 💰 SSN Token System

### Added
- **End-of-Game SSN Settlement**
  - SSN payouts are now settled once per run via `settle-ssn`.
- **Anti Double-Payout Protection**
  - Prevents duplicate payouts per user / track / season.
- **Blockchain Transaction Logging**
  - SSN transfers now record txid in backend.

### Fixed
- SSN not being transferred on-chain.
- SSN payouts not being recorded in database.
- Authorization handling between anon key (client) and service role (edge).

### Known Issue Resolved
- `payout_key` column mismatch in `ssn_payouts`
  - Schema updated or insert logic aligned with actual table columns.

---

## 🛠 Supabase Edge Functions

### `new-nft-drop`
- Fully rewritten and stabilized.
- Correct CORS handling.
- Proper Supabase client usage.
- Calls `send-nft` internally.
- Logs NFT drops to database.

### `send-nft`
- Verified invocation from `new-nft-drop`.
- Handles WAX NFT transfer.
- Records NFT sends.

### `settle-ssn`
- Rewritten for correctness and safety.
- Performs:
  - Authorization check
  - Anti-duplicate payout check
  - WAX SSN transfer
  - Database insert with txid
- Error handling improved with explicit logging.

---

## 🔐 Wallet Integration

### Fixed
- WAX login failures caused by UI state conflicts.
- Anchor login failures due to variable misuse and undefined references.
- Rescan button being disabled incorrectly after login.

### Improved
- Clear wallet badge (WAX / Anchor).
- Unified post-login flow for both wallet types.

---

## 📄 Documentation

### Added
- **Expanded Whitepaper**
  - Full rewrite from litepaper.
  - Includes Rhythm Master gameplay, SSN utility, NFT mechanics.
- **DAO Proposal Version**
  - Governance-focused version of whitepaper.
  - Suitable for WaxDAO or community voting.

---

## ⚠️ Notes
- SSN payouts require correct `ssn_payouts` schema alignment.
- NFT visibility depends on AtomicAssets API + valid metadata (audio/video fields).
- Users may need several seconds after purchase before NFTs appear via API.

---

## ✅ Overall Status
**Core gameplay, NFT drops, and SSN payouts are now fully wired end-to-end and production-ready.**

# Changelog (21/12/25)

## [Unreleased]

### Added
- Added **Re-scan Wallet** button to allow users to manually refresh their NFT inventory without reloading the page.
- Implemented wallet re-scan logic that re-fetches AtomicAssets NFTs and rebuilds the track dropdown.
- Added client-side guards to prevent duplicate NFT drop triggers per run.
- Added SSN accumulation per run and settlement call on game end.
- Added NFT win badge and optional transaction link in the Game Over screen.
- Added NFT pool support (`nft_pool` table) for controlled NFT drops.
- Added Supabase Edge Function `new-nft-drop` to:
  - Validate eligibility
  - Pick an unclaimed NFT
  - Call `send-nft`
  - Record drops in `nft_drops`
  - Mark NFTs as claimed
- Added extensive logging for NFT drops, SSN payouts, and analytics events.

### Changed
- Refactored NFT drop flow to be server-authoritative via Supabase Edge Functions.
- Updated game-end logic to reliably trigger SSN settlement.
- Improved IPFS media resolution with multiple gateway fallbacks.
- Updated wallet UI locking to clearly show WAX vs Anchor login state.
- Improved combo celebration overlays and NFT confetti effects.
- Alphabetically sorted NFT tracks in the dropdown for better UX.

### Fixed
- Fixed issue where SSN rewards were never settled due to missing end-game call.
- Fixed multiple cases of duplicated NFT drop requests from the client.
- Fixed Supabase Edge Function CORS and OPTIONS handling.
- Fixed `Illegal return statement` error in `new-nft-drop` by restructuring helper functions.
- Fixed missing `txid` propagation from `send-nft` to client UI.
- Fixed rescan button being disabled due to missing state re-enablement.
- Fixed cases where video-only NFTs were incorrectly filtered out.
- Fixed NFT dropdown not refreshing due to stale `tracks` state.
- Fixed Anchor/WAX login UI desyncs after failed authentication attempts.

### Known Issues
- Newly purchased NFTs may not appear immediately if:
  - The NFT is not in the expected collection
  - The NFT lacks required `audio`, `video`, or media metadata
  - AtomicAssets API caching delays occur
- Anchor login may fail in embedded browsers (Telegram, in-app browsers).
- Mobile Safari may block autoplay on first interaction.

### Notes
- NFT dropdown only shows **one entry per template ID** (deduplicated).
- NFTs without playable media (audio/video) are intentionally excluded.
- Service Role keys must **never** be exposed client-side.
- AtomicAssets API responses may lag behind recent marketplace purchases.

---  
_End of changelog_

# Changelog (21/12/25)

All notable changes to **Rhythm Master** will be documented in this file.

---

## [Unreleased]

### 🎮 Gameplay Improvements
- Added **rare NFT drop notes** (green pulsating bars) that can appear during gameplay.
- NFT notes display **“NFT”** on the bar and trigger a **large on-screen “N F T!” celebration** on a SUBLIME hit.
- Introduced **SSN reward notes**:
  - `1 × SSN`
  - `10 × SSN`
  - `100 × SSN`
- SSN notes glow and pulse in the same style as special multiplier notes.
- SSN rewards are **accumulated per run** and settled at game end.
- Added **SSN Earned** display to the Game Over screen.
- Added **“NFT WON” badge** to results when an NFT is successfully awarded.
- Added **confetti burst effect** when an NFT is won.

### 🧠 Difficulty & Feel
- Notes now **start slightly slower and gradually increase speed** over the duration of a track without breaking beat sync.
- Added a **small hit forgiveness buffer** to improve mobile play accuracy.
- Restart logic improved:
  - Up to **3 free restarts** per paid run.
  - Restarts do **not** record scores or require re-payment.
  - Payment is required again only after all restarts are exhausted.
- Visual restart counter added to the HUD.

### 🔐 Wallet & UX
- Login buttons (WAX + Anchor) now correctly **disable after login**, regardless of wallet type.
- Wallet badge (WAX / Anchor) added next to username and **properly centered**.
- “Pay 100 SSN for this track” text is now shown immediately after login when required.
- Caret (blinking text cursor) disabled globally for cleaner UI.
- Fullscreen mode now **only activates on mobile devices**, not desktop browsers.
- Improved Telegram handling with guidance to open in an external browser.

### 🏆 Leaderboards & Scoring
- Scores are only recorded when:
  - The player finishes normally, and
  - The score is higher than their previous best for that track.
- Restarted runs never overwrite leaderboard scores.
- Track list is now **sorted alphabetically**.

### 🪙 Token & NFT Payouts
- Implemented **server-side SSN settlement** via Supabase Edge Function:
  - Sends SSN from project wallet to player.
  - Records payouts in `ssn_payouts` table.
  - Prevents duplicate payouts per track/season.
- Implemented **secure NFT sending** via Supabase Edge Function:
  - Sends NFTs directly from the project wallet.
  - Enforces a **daily NFT send cap**.
  - Logs all sends in `nft_sends`.
- Added **NFT eligibility logic**:
  - Only SUBLIME hits qualify.
  - Max **1 NFT per player per season**.
  - Global cooldown between NFT drops.
  - Very low probability to ensure rarity.

### 🛡️ Security & Anti-Abuse
- All NFT and SSN transfers are **server-side only** (no private keys in frontend).
- Service Role Key is never exposed to the browser.
- Added safeguards against:
  - Double payouts
  - Rapid repeat NFT drops
  - Client-side tampering
- Split logic cleanly between:
  - Client trigger
  - Eligibility check
  - Secure transfer execution

### 🧩 Backend & Infrastructure
- Added new Supabase tables:
  - `nft_pool`
  - `nft_drops`
  - `nft_sends`
  - `ssn_payouts`
  - `analytics_events`
- Added analytics tracking for:
  - Wallet logins
  - SSN payments
  - Gameplay events
- Added Supabase Edge Functions:
  - `new-nft-drop`
  - `send-nft`
  - `settle-ssn`

---

## [Beta Notes]
- NFT drops are intentionally **extremely rare**.
- Some features (season pass, autograph NFTs) are scaffolded for future seasons.
- This build is intended for controlled beta testing before Season 1 launch.

---


# Changelog (21/12/25)

All notable changes to **Rhythm Master** will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project follows semantic versioning where applicable.

---

## [Unreleased]

### Added
- Admin-only **New Season** functionality using a dynamic `SEASON_ID`
- Persistent season tracking via `localStorage`
- Admin-only **Clear Track Leaderboard** button per track
- Secure leaderboard reset flow via Supabase Edge Function
- Admin UI visibility handling (`updateAdminUI`)
- Leaderboard auto-refresh after admin actions
- Unlimited restarts for admin accounts
- Improved leaderboard empty-state handling per season/track

### Changed
- Leaderboards are now scoped by **season + track**
- Season resets no longer delete historical data
- Admin users bypass SSN payment requirements
- Restart counter UI adapts based on admin status
- Leaderboard reloads automatically on track change

### Fixed
- Fixed missing click handler for admin season reset button
- Fixed duplicate `SEASON_ID` declaration causing script failure
- Fixed admin buttons not appearing after login
- Fixed missing `hitLine` DOM reference
- Prevented leaderboard reset actions from affecting other tracks
- Improved stability when switching tracks mid-session

---

## [0.9.0] – Beta Testing Phase

### Added
- Core rhythm gameplay loop
- Combo system with visual celebrations
- Dynamic multiplier notes (x2 / x3 / NFT)
- Supabase-powered global leaderboard
- Track-based scoring and ranking
- WAX & Anchor wallet login support
- SSN token payment gating per track
- NFT-trigger mechanics (drop & claim hooks)
- Mobile fullscreen + orientation handling
- Restart limits for non-admin players
- IPFS fallback loading for audio/video assets

### Known Issues
- Admin list is client-side only (server-side verification pending)
- NFT drop logic relies on external function availability
- No public season archive viewer yet

---

## Planned
- Admin control panel UI
- Server-side admin verification
- Season history & archive viewer
- Automated season rollover
- Per-track analytics dashboard

---

# Changelog (21/12/25)

All notable changes to Rhythm Master will be documented in this file.

---

## [Unreleased]

---

## [Beta – NFT Drop & Gameplay Systems Update]

### 🎮 Gameplay Enhancements
- Added **combo milestone celebrations**:
  - x5 → *NICE COMBO!* (green)
  - x10 → *GREAT COMBO!* (blue)
  - x20 → *AMAZING COMBO!* (larger)
  - x30 → *SUBLIME COMBO!* (pink)
  - x50 → *RHYTHM MASTER!* (legendary)
- Combo counter now increases **only on GREAT! and SUBLIME! hits**
- Multiplier visuals improved:
  - x2 → pulsating yellow circle
  - x3 → glowing red circle
- Notes now **start slightly slower and gently accelerate** over the track duration (visual only, beat sync preserved)
- Restart system implemented:
  - Up to **3 free restarts per track**
  - Restarts do **not submit scores**
  - After 3 restarts, payment is required again
  - Visual restart counter added to HUD
- Fixed muted audio issue on game start
- Prevented score submission when restarting mid-track

---

### 📱 Mobile & UX Improvements
- Game enters **fullscreen only on mobile devices**
- Prevented fullscreen triggering on desktop browsers
- Added orientation handling with pause/resume logic
- Disabled blinking text cursor globally
- Wallet badges visually centered and improved
- Wallet login buttons correctly disabled after login (WAX & Anchor)

---

### 🔐 Wallet & Payment Logic
- WAX Cloud Wallet login fully supported
- Anchor Wallet login added and stabilized
- Pay-per-track SSN system refined:
  - 100 SSN required per track (non-admin)
  - Admin users bypass payments
  - Payment UI correctly resets after game end
- Improved transaction error handling (successful tx despite WaxJS warnings)

---

### 🎵 NFT & Track Handling
- NFT track list deduplicated by template ID
- Tracks populated from AtomicAssets using normalized IPFS CIDs
- IPFS gateway fallback system added for audio, video, and images
- Track dropdown now supports:
  - Audio-only NFTs
  - Video-only NFTs
- Track visuals correctly prioritize video with image fallback
- Background media unmuted correctly on user interaction

---

### 🏆 Leaderboards & Backend
- Supabase leaderboard integration stabilized
- Scores only update if higher than previous personal best
- Leaderboards scoped by **season + track**
- Added tracking for max combo per score entry

---

### 🟢 Rare NFT Drop System (NEW)
- Designed and implemented **rare in-game NFT drop mechanic**
- Added new **green “NFT” note type** (very rare spawn)
- NFT drop only triggers on **SUBLIME! hit**
- Drop logic split into two stages for security:
  1. Client-side trigger (no wallet secrets)
  2. Supabase Edge Function for actual NFT transfer
- Implemented **Supabase Edge Function: `send-nft`**
  - Uses project wallet to transfer NFTs
  - Restricted via Service Role key
  - Enforces **daily send cap**
  - Logs all sends to `nft_sends` table
- NFT selection:
  - Random NFT
  - From `sublimesound` collection
  - **Mythic rarity only**
- Test mode toggle supported (safe dry runs)

---

### 🛡️ Security & Fair Play
- Added daily NFT send cap to limit abuse
- Server-side authority for NFT transfers
- Asset ownership controlled entirely off-client
- Prevented duplicate NFT rewards per trigger
- Prepared hooks for future anti-bot extensions

---

### 🧱 Infrastructure & Developer Experience
- Supabase tables designed for:
  - Leaderboards
  - NFT send logs
  - Analytics expansion
- Improved error logging across game loop and backend
- Refactored wallet state handling to avoid UI desyncs

---

### 🐞 Bug Fixes
- Fixed lanes disappearing after refactors
- Fixed muted playback regression
- Fixed Anchor blockchain ID errors
- Fixed repeated NFT listings in track selector
- Fixed score submission edge cases on restart
- Fixed payment text showing during free restarts
- Fixed fullscreen behavior on desktop browsers

---

## Notes
This update introduces the foundation for **on-chain reward drops tied directly to gameplay skill**, while maintaining strong security guarantees and player fairness.

Future work will expand NFT eligibility rules, rarity tuning, analytics dashboards, and DAO-governed reward parameters.

# Changelog (18/12/25)

All notable changes to **Rhythm Master** will be documented in this file.

---

## [Unreleased] – Beta Improvements (Mobile, Gameplay & UX)

### 🎮 Gameplay Changes
- Added **hit window forgiveness buffer** for mobile players  
  - Introduced `HIT_BUFFER` to reduce false MISS judgments on touch devices
- Improved **note-to-hitline alignment**
  - Notes now calculate position relative to the actual hit line instead of hardcoded values
- Falling notes now **start slightly slower and accelerate gradually** during a track
  - Visual speed scaling does not affect beat timing or score accuracy
- Combo logic updated:
  - Combos now increment on **GREAT! and SUBLIME! hits only**
  - Combo resets correctly on MISS or OK hits

---

### 🔁 Restart System
- Added **free restart system** per track:
  - Players get **3 free restarts** without paying SSN again
  - Restarting does **not submit scores**
- Added **visual restart counter** (`Restarts left: X / 3`)
- Restart button automatically:
  - Disappears after all free restarts are used
  - Requires SSN payment again once exhausted
- Fixed logic so:
  - Clicking **OK (not restart)** submits score (if higher than previous)
  - Payment is required again after a completed run

---

### 📱 Mobile & Fullscreen Experience
- Game now enters **fullscreen mode** automatically when starting a track
- Added **landscape orientation lock** during gameplay (where supported)
- Implemented **rotate device overlay hint** for mobile portrait mode
- Game pauses/resumes automatically when device orientation changes
- Prevented page scrolling and gesture conflicts during gameplay
- Disabled blinking text cursor (`caret`) globally for cleaner visuals

---

### 🎨 Visual & UI Enhancements
- Added new combo celebrations:
  - **x5** → NICE COMBO! (green)
  - **x10** → GREAT COMBO! (blue)
  - **x20** → AMAZING COMBO!
  - **x30** → SUBLIME COMBO!
  - **x50** → RHYTHM MASTER! (gold, large)
- Combo celebrations:
  - Centered on screen
  - Fade automatically after ~2 seconds
- Multiplier indicator improvements:
  - x2 → Pulsing yellow glow
  - x3 → Glowing red pulse
- Wallet badge improvements:
  - Text is now perfectly centered inside badge
  - Badge shows connected wallet type (WAX / Anchor)
- Login buttons now correctly:
  - Disable once logged in (WAX or Anchor)
  - Prevent duplicate login attempts

---

### 🔊 Audio / Media
- Fixed muted playback issues:
  - Audio and video now explicitly unmute after user interaction
- Improved IPFS media loading reliability:
  - Audio and video use gateway fallback system
- Video-only tracks now start correctly without audio dependency

---

### 🧾 Payments & Access
- SSN payment now enforced **per track**
- Payment status text correctly updates based on state:
  - Initial login
  - Free restart usage
  - Post-game completion
- Admin users:
  - Bypass SSN payment
  - Have unlimited restarts
  - See admin-only controls

---

### 🏆 Leaderboards
- Scores are now:
  - Submitted only on valid completed runs
  - Rejected if lower than player’s existing best score
- Leaderboard refreshes automatically after submission
- Restarted runs do not affect leaderboard data

---

### 🐛 Bug Fixes
- Fixed false MISS detections caused by fullscreen scaling
- Fixed note alignment issues after fullscreen/orientation changes
- Fixed restart logic incorrectly requiring payment
- Fixed combo counter persisting across restarts
- Fixed login UI inconsistencies between WAX and Anchor
- Fixed duplicate NFT template loading edge cases

---

## Notes
- All changes are backward compatible with existing seasons
- No contract changes required
- Mobile experience significantly improved in this release

---

# Changelog (17/12/25)

All notable changes to **Rhythm Master** will be documented in this file.

---

## [Unreleased]

### Added
- 🎵 **Free Restart System**
  - Players may restart the same track **up to 3 times** without repaying SSN.
  - Restart counter displayed in HUD.
  - Restart button disappears after all retries are exhausted.
  - Admin users have unlimited restarts.

- 🔁 **Restart Visual Counter**
  - HUD shows remaining restarts (e.g. `Restarts left: 2 / 3`).
  - Counter dims when no restarts remain.

- 🔥 **Combo Milestones**
  - x5 → NICE COMBO!
  - x10 → GREAT COMBO!
  - x20 → AMAZING COMBO!
  - x30 → SUBLIME COMBO!
  - x50 → RHYTHM MASTER!
  - Combo celebrations appear center-screen with animated glow.

- 🎯 **Combo Logic Update**
  - Combos now increment **only on GREAT and SUBLIME hits**.
  - Combo resets on OK or MISS.

- ✨ **Dynamic Multiplier UI**
  - x1 shown in neutral circle.
  - x2 activates pulsing yellow multiplier circle.
  - x3 activates glowing red multiplier circle.
  - Visuals persist only while multiplier is active.

- 🐢➡️⚡ **Dynamic Note Speed**
  - Notes fall slightly slower at the start of a track.
  - Speed gradually increases over time.
  - Beat timing remains unchanged (pure visual scaling).

- 🎥 **Video-Only Track Support**
  - Tracks with video but no audio now play correctly.
  - Beat timing derived from video duration.

- 🔊 **Audio Autoplay Fix**
  - Ensures audio and video unmute correctly on user interaction.
  - Prevents muted playback after restart or login.

- 🧠 **IPFS Gateway Fallback System**
  - Automatic fallback across multiple IPFS gateways for audio, video, and images.
  - Improves reliability and load success for NFT media.

- 🧩 **NFT De-duplication**
  - Prevents duplicate tracks by template ID.
  - Upgrades missing images if a later asset provides one.

- 🔐 **Wallet Improvements**
  - Anchor Wallet support added alongside WAX Cloud Wallet.
  - Login buttons correctly disable during gameplay.

- 🏆 **Leaderboard Improvements**
  - Scores only submitted on completed runs.
  - Restarted runs do NOT submit scores.
  - Higher score always preserved per user/track/season.

---

### Fixed
- 🐞 Restarting no longer consumes SSN.
- 🐞 Payment message no longer shows during free restarts.
- 🐞 Combo counter no longer increments on OK hits.
- 🐞 Blinking text cursor removed globally.
- 🐞 Lanes disappearing bug resolved.
- 🐞 Muted playback bug resolved.
- 🐞 Anchor blockchain ID configuration issue resolved.
- 🐞 Duplicate NFT track entries resolved.
- 🐞 Leaderboard submission triggering incorrectly on restart fixed.

---

### Changed
- Restart logic refactored to cleanly separate:
  - Paid runs
  - Free restarts
  - Exhausted retry states

# 📝 Changelog – Rhythm Master (17/12/25)

## 🚀 New Features

### 🎮 Gameplay & Scoring
- Added **combo-based celebration system** with animated on-screen text:
  - **5x Combo** → *NICE COMBO!* (green)
  - **10x Combo** → *GREAT COMBO!* (blue)
  - **20x Combo** → *AMAZING COMBO!* (larger text)
  - **30x Combo** → *SUBLIME COMBO!* (large pink)
  - **50x Combo** → *RHYTHM MASTER!* (legendary, gold)
- Combo celebrations display centrally with glow + fade animation (~2s).
- Combos now **only build from GREAT and SUBLIME hits**.
- Combo counter resets correctly on OK / MISS hits.
- Score calculation adjusted to weight:
  - SUBLIME > GREAT > OK
- Multiplier notes (x2 / x3) visually enhanced and fully integrated with scoring.

### 🎵 Media & IPFS
- Robust **IPFS gateway fallback system** for audio and video:
  - Multiple Pinata + Cloudflare + ipfs.io gateways
- Supports **audio-only**, **video-only**, and **audio+video** NFTs.
- Automatic unmute handling on game start to avoid silent playback.
- Improved video-only track startup reliability.

### 🧾 Payments & Economy
- **Per-track SSN payment system**:
  - Non-admin users must pay **100 SSN per track play**
  - Payment resets when switching tracks
- Admin accounts bypass payment logic entirely.
- Improved SSN payment UX:
  - Disabled buttons during processing
  - Success + fallback confirmation handling
- Added transaction link to WaxBlock explorer after payment.

### 👛 Wallet Support
- Dual wallet support:
  - **WAX Cloud Wallet**
  - **Anchor Wallet**
- Separate login buttons for WAX and Anchor.
- Unified gameplay flow regardless of wallet type.
- Wallet buttons disabled appropriately during gameplay to prevent conflicts.

### 🏆 Leaderboards (Server-Side)
- Migrated leaderboard from localStorage to **Supabase backend**.
- Server-side leaderboard features:
  - Per-season
  - Per-track
  - Top 10 ranking
  - Stores score, max combo, and user account
- Only higher scores overwrite existing entries.
- Leaderboard auto-refreshes on track change and game end.

### 🎨 UI / UX Improvements
- Centralized combo overlay layer (always on top).
- Improved visual feedback for:
  - SUBLIME / GREAT / OK / MISS
  - Lane hit animations
  - Screen shake on SUBLIME hits
- Disabled login buttons during active gameplay.
- Cleaner game-over flow with restart support.

---

## 🐛 Bug Fixes

- Fixed muted audio/video on game start.
- Fixed video-only tracks not starting gameplay.
- Fixed combo counter incrementing on incorrect hits.
- Fixed leaderboard not updating after game end.
- Fixed duplicate NFTs appearing in track list by:
  - De-duplicating via **template_id**
  - Merging media fields safely
- Fixed repeated note DOM buildup by clearing notes on game end.
- Fixed payment flow edge cases where WaxJS throws after successful transaction.
- Improved orientation pause/resume stability on mobile.

---

## ⚙️ Configuration & Toggles

- Added `ENABLE_SEASON_PASS` flag to quickly enable/disable season pass checks.
- Admin list centralized for easier permission control.
- Improved IPFS CID normalization across all NFT schemas.

---

## ⚠️ Known Issues / Work in Progress

- Anchor Wallet may show **“Unknown Blockchain ID”** warnings depending on chain configuration.
- Anchor chain handling requires further stabilization and testing.
- Some edge-case NFT schemas may still require manual mapping.
- Server-side leaderboard anti-cheat and validation pending.

---

## 🗺️ Coming Next
- Autographed NFT score modifiers
- Fair play / advantage disclosure
- Season-based rewards & DAO integration
- Hardened Anchor wallet flow
- Anti-cheat validation on leaderboard submissions

# 📝 Changelog / Patch Notes (16/12/25)

## [Beta] – Current Development Cycle

### ✅ Added
- GREAT + SUBLIME combo eligibility
- Combo milestone celebrations (10 / 20 / 30)
- Per-track SSN payment system
- Admin bypass for payments
- Season pass toggle flag
- Video-only NFT track support
- IPFS multi-gateway fallback
- Per-template NFT de-duplication
- Improved mobile orientation handling

---

### 🐞 Fixed
- Muted audio/video on start
- Duplicate NFT track listings
- Video-only tracks not starting
- WaxJS false-negative payment errors
- Combo counter desync
- Background image fallback issues
- Login UI lockups after gameplay

---

### ⚙️ Changed
- Combo logic simplified & more forgiving
- GREAT hits now count toward combos
- Cleaner admin vs player permission logic

---

### 🧪 Known Issues
- Some NFT images missing metadata (to be resolved)
- Certain AtomicAssets schemas incomplete

---

More updates coming soon.

# 🎵 Sublime Sounds – Rhythm Master  
## Development Log / Changelog (16/12/25)

---

## ✅ New Features

### 🎮 Gameplay Enhancements
- **Combo Celebrations Added**
  - `10x SUBLIME hits` → **GREAT COMBO!** (blue)
  - `20x SUBLIME hits` → **AMAZING COMBO!** (larger blue)
  - `30x SUBLIME hits` → **SUBLIME COMBO!** (large pink)
  - Animations display center-screen for ~2 seconds
  - Uses dedicated overlay layer to ensure visibility above all UI

- **SUBLIME-Only Combo Logic**
  - Combo counter **only increases on SUBLIME hits**
  - OK / MISS immediately resets combo
  - Combo milestone tracking prevents duplicate celebration spam

- **Improved Hit Feedback**
  - Stronger visual feedback for SUBLIME hits
  - Refined screen shake + spark effects

---

## 💳 Payment System Improvements

### Per-Track Payment Logic
- Users must pay **100 SSN per track**
- Payment resets when switching tracks
- Payment required again after each completed game (non-admins)

### Admin Bypass
- Admin wallets:
  - Bypass SSN payment
  - Payment button hidden
  - Start button always enabled

### Payment UX Improvements
- Pay button disabled while processing
- Success/failure feedback added
- Transaction link displayed on success

---

## 🔐 WAX Login & Session Handling

- Fixed incorrect wallet assignment
  - Switched to `wax.userAccount` (reliable)
- Login button disabled during gameplay
- Login restored after game end
- Improved error handling for failed login attempts

---

## 🎶 Media & Playback Fixes

- **Unmuted Audio on Game Start**
  - Explicit unmute + volume restore for audio & video
- Improved IPFS gateway fallback for audio & video
- Robust handling for:
  - Audio-only tracks
  - Video-only tracks
  - Mixed media tracks

---

## 🖼️ NFT Track Loading Improvements

### AtomicAssets Integration
- Fetches NFTs by:
  - Owner
  - Collection name
- Supports audio, video, animation, and media fields

### Duplicate Prevention
- Tracks deduplicated by **template_id**
- First valid asset per template used
- Later assets can backfill missing image data

### Metadata Handling
- Safely merges:
  - `template.immutable_data`
  - `asset.data`
- Supports:
  - `audio`
  - `video`
  - `animation_url`
  - `image / img / media`

---

## 🧠 Game State Stability

- Notes cleared correctly on:
  - Game end
  - Restart
- Prevents duplicate note spawning
- Fixed paused/resumed state when rotating mobile devices
- Ensured game loop stops cleanly on end

---

## 📱 Mobile & UX Improvements

- Orientation lock overlay added for mobile portrait mode
- Game auto-pauses on invalid orientation
- Touch gestures locked only during gameplay
- Improved button disabling to prevent accidental actions

---

## 🏆 Leaderboard

- Per-track leaderboard keys
- Scores stored locally
- Higher score replaces previous score for same user
- Sorted descending, top 10 only

---

## 🐞 Bugs Fixed

- Muted audio/video on play
- Combo counter incrementing on non-SUBLIME hits
- Duplicate NFTs appearing in track list
- Admins incorrectly required to pay
- Login button active during gameplay
- Notes persisting after game end
- Inconsistent media loading from IPFS gateways

---

## ⚠️ Known Issues (To Address Later)

- Some templates still missing background images
  - Likely inconsistent AtomicAssets metadata
  - Requires deeper per-template inspection
- Some video-only templates still inconsistent across gateways

---

## 🛠️ Next Steps (Planned)

- Alphabetical track sorting
- Improved fallback image logic
- Template-level debugging tool
- Server-side leaderboard
- Visual track previews in selector

# Changelog
All notable changes to **Rhythm Master** will be documented in this file.

This project follows **Semantic Versioning**:  
`MAJOR.MINOR.PATCH`  
and is currently in **Beta**.

---

## [0.9.0] – Beta Release Candidate  
**Status:** Feature-complete beta  
**Date:** 2025-09-15

### Added
- Mobile orientation detection with **pause-on-rotate**
- Full-screen rotate-device overlay during gameplay
- Automatic resume when returning to landscape
- Non-looping video NFT backgrounds (game ends with video)
- START_DELAY before notes spawn
- Multiplier pickup notes (x2 / x3)
- Screen flash effect on multiplier activation
- Restart button on Game Over screen
- Local leaderboard persistence per track & season
- Admin wallet bypass for Season Pass requirement
- Ad slot layout (6 slots + branded placements)
- Dynamic NFT track loading (audio / video / image priority)

### Changed
- Improved mobile touch handling (pointer events only during play)
- Refactored scroll-lock logic to avoid page freeze on mobile
- Gameplay loop now safely pauses during orientation changes
- Start button gated behind Season Pass NFT ownership
- Video NFTs take priority over static images when both exist
- Audio/video playback synced to gameplay loop

### Fixed
- iOS Safari scrolling freeze during gameplay start
- Lost lane hit effects (pulse, sparks, shake)
- Muted background video playback
- Notes persisting after game end
- WAX login failures caused by reinitialisation
- Restart logic resetting multipliers and timers correctly

---

## [0.8.0] – Mobile Stability & UX Update  
**Date:** 2025-08-XX

### Added
- Mobile-only rotate-for-best-experience hint
- Tablet viewport scaling safeguards
- Visual hit judgements (SUBLIME / OK / MISS)
- Lane pulse animations and camera shake
- Background image support per NFT track

### Changed
- Improved viewport meta configuration
- Refined touch-action rules for lanes vs page
- Reduced accidental gesture blocking on mobile

### Fixed
- Lane interaction not registering on some Android devices
- Judge text not appearing on perfect hits
- Game loop desync on slower devices

---

## [0.7.0] – NFT & WAX Integration  
**Date:** 2025-07-XX

### Added
- WAX Cloud Wallet login
- NFT ownership detection via AtomicAssets API
- Track selection from owned NFTs
- Season Pass NFT gating (template-based)
- Admin wallet override
- Local leaderboard storage

### Changed
- Start button disabled until wallet login
- Track selector locked until NFTs are loaded

### Fixed
- WAX login state resetting on UI changes
- Track selector breaking login flow

---

## [0.6.0] – Core Gameplay  
**Date:** 2025-06-XX

### Added
- Rhythm gameplay engine
- Falling note system
- Accuracy-based scoring
- Combo tracking
- Multiplier HUD
- Game Over overlay

### Changed
- Timing window tuned for mobile input latency

---

## [0.5.0] – Visual Foundation  
**Date:** 2025-05-XX

### Added
- Lane system (5 lanes)
- Hit line
- Background container
- Spark hit effects
- Sublime Sounds branding

---

## [0.4.0] – Initial Prototype  
**Date:** 2025-04-XX

### Added
- Basic UI layout
- Static lanes
- Placeholder scoring
- Early concept visuals

---

## Planned
- Cloud-backed leaderboards
- Player profiles & progression
- Achievements & mintable rewards
- Multiplayer modes
- PWA support
- Anti-cheat & analytics
- Seasonal events

---

**Maintained by:** Sublime Sounds  
**Project:** Rhythm Master  
**Status:** Beta (Pre-Launch)
