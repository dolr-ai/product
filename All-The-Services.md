# All The Services – API Inventory

| API Name | API Type | Method | Description | API Developer | Maintainer | API Health | Complexity (1–5) | Needs Rework (1–5) | Notes |
|---|---|---|---|---|---|---|---|---|---|
| Off Chain | Backend | — | Routes that were initially not possible to keep in canister: VideoGen, event streaming, video deduplication, etc. | Initially Komal, then Joel | Joel | Fair | 3 | 5 | — |
| Yral Auth | Backend | — | Manages all things related to login and authentication | Rupansh, then Ravi | — | Good | 4 | 1 | — |
| Backend Canisters | ICP Canister | — | Stores and provides APIs for rate limits in video gen, user details, and post details | Ravi | Ravi | Good | 4 | 1 | — |
| YRAL Metadata | Backend | — | Stores and provides mapping from user principal to username, notification keys, and provides a way to send notifications | Initially Rupansh | Joel, Ravi | Good | 2 | 2 | — |
| Yral AI Chat | Backend / AI | — | APIs to create, chat and view the AI-Influencer | Kevin | Joel (To be transitioned) | Fair | 4 | 4 | Reworking on switching DB since most latency issues are caused from the db |
| Yral Storage Service | Backend | — | Storage service for handling hetzner and storj uploads | Initially Tushar, then Joel | Joel | Good | 2 | 3 | — |
| AI Video Agent | AI | — | Gradio-powered agent for orchestrating AI influencer video content generations | Kevin | Joel (To be transitioned) | Good | 2 | 2 | — |
| Yral ML Feed Server | AI | — | Recommendations feed and tournament | Jay | Adarsh (To be transitioned) | Good | 4 | 2 | Reworking on implementing a caching layer and reducing latency |
| Yral NSFW Classification | AI | — | Content Moderation Service | Jay | Adarsh (To be transitioned) | Good | 4 | 1 | This API also detects borderline provocative content. A nudity-only classifier may also be needed |
| /cast_vote_v2 | Backend | POST | Cast emoji vote on a video. Params: principal_id, video_id, smiley_id. Win = match majority emoji (+3 coins), Loss = -1 coin. Has fraud detection (15k/day limit). | Samarth | Sarvesh | Good | 3 | 1 | — |
| /tap_to_recharge | Backend | POST | Auto-recharge balance when it hits zero (max 2 times, +25 coins). Params: principal_id. | Samarth | Sarvesh | Good | 1 | 1 | — |
| /v2/balance/{principal_id} | Backend | GET | Get user's YRAL token balance. Base URL: yral-hot-or-not.go-bazzinga.workers.dev | Samarth | Sarvesh | Good | 2 | 1 | — |
| /cast_hot_or_not_vote | Backend | POST | Vote "hot" or "not" on a video. Params: principal_id, video_id, vote. Win = match majority vote (+1 coin), Loss = -1 coin. | Sarvesh | Sarvesh | Good | 3 | 1 | — |
| /tournaments | Backend | POST | List tournaments with filters. Params: date, status, principal_id, tournament_id, type ("smiley"/"hot_or_not"). | Sarvesh | Sarvesh | Good | 3 | TBD | Needs rework — score TBD |
| /tournament_status | Backend | POST | Lightweight tournament status check. Params: tournament_id. Returns status, participant_count, time_left_ms. | Sarvesh | Sarvesh | Good | 3 | TBD | Needs rework — score TBD |
| /register_for_tournament | Backend | POST | Register & pay entry fee. Params: tournament_id, principal_id, is_pro. Gives 20 initial diamonds. | Sarvesh | Sarvesh | Good | 3 | 1 | — |
| /my_tournaments | Backend | POST | Get tournaments user has played in. Params: principal_id. | Sarvesh | Sarvesh | Good | 4 | 1 | — |
| /tournament_leaderboard | Backend | POST | Get leaderboard & user position. Params: tournament_id, principal_id. Ranked by diamonds > total games > updated_at. | Sarvesh | Sarvesh | Good | 4 | TBD | Needs rework — score TBD |
| /tournament_vote | Backend | POST | Cast emoji vote in tournament. Params: tournament_id, principal_id, video_id, smiley_id. Win = match majority emoji (+1 diamond), Loss = -1 diamond. Can't vote at 0 diamonds. | Sarvesh | Sarvesh | Good | 3 | 1 | — |
| /tournament_video_emojis | Backend | POST | Get emojis for a specific video. Params: tournament_id, video_id. Used for prefetching. | Sarvesh | Sarvesh | Good | 4 | 1 | — |
| /hot_or_not_tournament_vote | Backend | POST | Vote hot/not vs AI verdict. Params: tournament_id, principal_id, video_id, vote. Win = match Gemini AI's verdict (+1 diamond), Loss = -1 diamond. | Sarvesh | Sarvesh | Good | 3 | 1 | — |
| /start_daily_session | Backend | POST | Start/resume daily tournament session (auto-registers if needed). Params: tournament_id, principal_id. Returns remaining_time_ms, diamonds, wins, losses. | Sarvesh | Sarvesh | Good | 3 | 1 | — |
| /end_daily_session | Backend | POST | End current session (on exit). Params: tournament_id, principal_id. Returns time_spent_ms, remaining_time_ms. | Sarvesh | Sarvesh | Good | 3 | 1 | — |
| /create_tournaments | Backend | POST | Create smiley tournaments. Fetches videos from recsys, analyzes with Gemini for emoji selection, seeds initial votes, schedules Cloud Tasks. | Sarvesh | Sarvesh | Good | 4 | 1 | Admin only |
| /create_hot_or_not_tournament | Backend | POST | Create Hot or Not tournament. Fetches videos, analyzes with Gemini 2.0 Flash for hot/not verdicts, ensures ~50/50 distribution. | Sarvesh | Sarvesh | Good | 4 | 1 | Admin only |
| /update_tournament_status | Backend | POST | Advance tournament lifecycle (scheduled → live → ended → settled). Handles prize settlement & BTC payouts. Triggered by Cloud Tasks. | Sarvesh | Sarvesh | Good | 4 | 1 | Admin only |
