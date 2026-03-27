# YRAL Analytics Events Reference

Complete reference of all analytics events tracked in the YRAL mobile app. Each event includes a `event` field (the event name) and a `feature_name` field (the category) in addition to the properties listed below.

---

## App

| Event Name | Description | Properties |
|---|---|---|
| `first_app_launch` | When the app is launched for the first time | `date_time` (String) |
| `splash_screen_viewed` | When splash screen is shown | — |
| `app_onboarding_shown` | When an onboarding step is shown to the user | `onboarding_step` (AnalyticsOnboardingStep) |

**AnalyticsOnboardingStep**: `game_intro_start`, `balance_intro`, `rank_intro`, `game_intro_end`

---

## Auth / Signup / Login

| Event Name | Description | Properties |
|---|---|---|
| `auth_screen_viewed` | When the user sees the signup screen | `page_name` (SignupPageName) |
| `signup_clicked` | When user clicks on the Login CTA | `page_name` (SignupPageName) |
| `signup_journey_selected` | When user clicks on either signup with Google or signup with Apple | `auth_journey` (AuthJourney) |
| `signup_initiated` | When signup/login is initiated | `auth_journey` (AuthJourney) |
| `signup_success` | When new user signs up successfully | `is_referral` (Boolean)<br>`referrer_user_id` (String)<br>`auth_journey` (AuthJourney)<br>`affiliate` (String?) |
| `login_success` | When existing user logs in successfully | `auth_journey` (AuthJourney)<br>`affiliate` (String?) |
| `auth_failed` | On authentication failure | `auth_journey` (AuthJourney)<br>`affiliate` (String?) |
| `anonymous_auth_failed` | On anonymous authentication failure | `affiliate` (String?)<br>`reason` (String?) |
| `auth_session_state_changed` | When the authentication session state changes | `from_state` (AuthSessionState)<br>`to_state` (AuthSessionState)<br>`initiator` (AuthSessionInitiator)<br>`cause` (AuthSessionCause)<br>`flow` (AuthSessionFlow?) |
| `identity_transition` | When the user's distinct ID changes (e.g., anonymous to authenticated) | `previous_distinct_id` (String)<br>`new_distinct_id` (String)<br>`reset_reason` (String) |
| `signup_nudge_dismissed` | User dismisses login nudge | `dismiss_action` (SignupNudgeDismissAction) |
| `phone_number_entered` | User enters phone number | `country_code` (String)<br>`phone_length` (Int) |
| `otp_request_initiated` | User requests OTP | `attempt_number` (Int)<br>`request_type` (OtpRequestType) |
| `otp_screen_viewed` | OTP screen displayed | `phone_number` (String) |
| `otp_validation_result` | OTP verification result | `validation_status` (OtpValidationStatus)<br>`failure_reason` (String?)<br>`phone_number` (String) |
| `otp_dismissed` | User dismisses the OTP screen | — |

**AuthJourney**: `google`, `apple`, `phone`

**SignupPageName**: `splash`, `home`, `menu`, `conversation`, `profile`, `video_creation`, `upload_video`, `leaderboard`, `tournament`, `create_influencer`

**AuthSessionState**: `authenticated`, `unauthenticated`

**AuthSessionInitiator**: `user`, `system`

**AuthSessionCause**: `refresh_token_missing`, `refresh_token_expired_or_invalid`, `refresh_access_token_failed`

**AuthSessionFlow**: `token_validation`, `token_refresh`

**SignupNudgeDismissAction**: `close`, `skip`

**OtpRequestType**: `initial`, `resend`

**OtpValidationStatus**: `success`, `failure`

---

## Home / Feed

| Event Name | Description | Properties |
|---|---|---|
| `home_page_viewed` | When user lands on the home page | `affiliate` (String?) |
| `bottom_navigation_clicked` | When user clicks on any bottom nav | `category_name` (CategoryName) |
| `feed_toggle_clicked` | When user clicks on the feed type toggle | `feed_type` (FeedType)<br>`is_expanded` (Boolean) |
| `feed_loader_shown` | When the feed loading indicator is shown | `duration_ms` (Long) |

**CategoryName**: `upload_video`, `leaderboard`, `tournaments`, `profile`, `menu`, `home`, `refer_and_earn`, `wallet`, `chatbot`

**FeedType**: `default`, `ai`, `nsfw`

---

## Video

| Event Name | Description | Properties |
|---|---|---|
| `video_started` | When the video starts playing | `video_id` (String)<br>`publisher_user_id` (String)<br>`like_count` (Long)<br>`share_count` (Long)<br>`view_count` (Long)<br>`is_game_enabled` (Boolean)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean) |
| `video_impression` | When a new video appears on the screen, even if it hasn't started playing yet | `video_id` (String)<br>`publisher_user_id` (String)<br>`like_count` (Long)<br>`share_count` (Long)<br>`view_count` (Long)<br>`is_game_enabled` (Boolean)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean) |
| `video_viewed` | When the video is watched for >= 3 seconds | `video_id` (String)<br>`publisher_user_id` (String)<br>`like_count` (Long)<br>`share_count` (Long)<br>`view_count` (Long)<br>`is_game_enabled` (Boolean)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean) |
| `video_clicked` | When user interacts with any CTA/icon on the video | `video_id` (String)<br>`publisher_user_id` (String)<br>`like_count` (Long)<br>`share_count` (Long)<br>`view_count` (Long)<br>`is_game_enabled` (Boolean)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean)<br>`cta_type` (CtaType)<br>`page_name` (CategoryName) |
| `nsfw_enabled` | When user clicks on "I agree" on the NSFW popup | `page_name` (String) |
| `video_reported` | When user reports the video successfully | `video_id` (String)<br>`publisher_user_id` (String)<br>`is_game_enabled` (Boolean)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean)<br>`report_reason` (String) |
| `delete_video_initiated` | When user clicks on delete CTA on confirmation popup | `page_name` (CategoryName)<br>`video_id` (String) |
| `video_deleted` | When video gets deleted successfully | `page_name` (CategoryName)<br>`video_id` (String)<br>`cta_type` (VideoDeleteCTA) |
| `video_downloaded` | When user downloads a video | `video_id` (String) |
| `video_duration_watched` | Detailed video watch duration tracking | `canister_id` (String)<br>`creator_category` (String)<br>`display_name` (String)<br>`feed_type` (String)<br>`hashtag_count` (Int)<br>`is_hot_or_not` (Boolean)<br>`is_logged_in` (Boolean)<br>`is_nsfw` (Boolean)<br>`like_count` (Long)<br>`post_id` (String)<br>`publisher_canister_id` (String)<br>`publisher_user_id` (String)<br>`share_count` (Long)<br>`user_id` (String)<br>`video_category` (String)<br>`video_id` (String)<br>`view_count` (Long)<br>`nsfw_probability` (Double)<br>`absolute_watched` (Double)<br>`percentage_watched` (Double)<br>`video_duration` (Double) |

**GameType**: `hot_or_not`, `smiley`

**CtaType**: `like`, `share`, `refer_and_earn`, `report`, `creator_profile`, `nsfw_toggle`, `mute`, `unmute`, `delete`, `video_play`, `follow`, `unfollow`

**VideoDeleteCTA**: `profile_thumbnail`, `video_fullscreen`

---

## Game

| Event Name | Description | Properties |
|---|---|---|
| `game_voted` | When user votes/plays any game (e.g., Hot or Not, Smiley) | `video_id` (String)<br>`publisher_user_id` (String)<br>`like_count` (Long)<br>`share_count` (Long)<br>`view_count` (Long)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean)<br>`stake_amount` (Int)<br>`stake_type` (TokenType)<br>`option_chosen` (String)<br>`is_tutorial_vote` (Boolean)<br>`swipe_action` (SwipeAction?) |
| `how_to_play_clicked` | When user clicks on the "?" help icon | `game_type` (GameType) |
| `game_played` | When game is concluded | `video_id` (String)<br>`publisher_user_id` (String)<br>`like_count` (Long)<br>`share_count` (Long)<br>`view_count` (Long)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean)<br>`stake_amount` (Int)<br>`stake_type` (TokenType)<br>`option_chosen` (String)<br>`conclusion` (GameResult)<br>`won_loss_amount` (Int)<br>`is_tutorial_vote` (Boolean)<br>`affiliate` (String?) |
| `game_concluded_bottomsheet_clicked` | When user clicks on either "keep playing" or "learn more" on the game result bottom sheet | `stake_amount` (Int)<br>`stake_type` (TokenType)<br>`conclusion` (GameResult)<br>`won_loss_amount` (Int)<br>`cta_type` (GameConcludedCtaType) |
| `game_tutorial_shown` | When game tutorial is shown | `video_id` (String)<br>`publisher_user_id` (String)<br>`like_count` (Long)<br>`share_count` (Long)<br>`view_count` (Long)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean) |
| `forced_gameplay_nudge_shown` | When Forced Gameplay Nudge is shown to user | `video_id` (String)<br>`publisher_user_id` (String)<br>`like_count` (Long)<br>`share_count` (Long)<br>`view_count` (Long)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean) |

**TokenType**: `cents`, `sats`, `yral`

**GameResult**: `win`, `loss`

**GameConcludedCtaType**: `keep_playing`, `learn_more`

**SwipeAction**: `swipe`, `click`

---

## Menu

| Event Name | Description | Properties |
|---|---|---|
| `menu_page_viewed` | When user lands on the menu page | — |
| `menu_clicked` | When user clicks on any of the CTAs on the menu page | `cta_type` (MenuCtaType) |

**MenuCtaType**: `login`, `talk_to_the_team`, `terms_of_service`, `privacy_policy`, `log_out`, `delete_account`, `follow_on`

---

## Upload Video

| Event Name | Description | Properties |
|---|---|---|
| `upload_video_page_viewed` | When user lands on upload video page | — |
| `video_creation_page_viewed` | When user lands on the video creation page (AI or upload) | `type_ext` (VideoCreationType)<br>`credits_fetched` (Boolean?)<br>`credits_available` (Int?) |
| `select_file_clicked` | When user clicks select file | — |
| `file_selection_success` | When user successfully selects a file | `file_type` (String) |
| `video_upload_initiated` | When user clicks on upload CTA and video upload is initiated | `caption_added` (Boolean)<br>`hashtags_added` (Boolean)<br>`type_ext` (VideoCreationType)<br>`affiliate` (String?) |
| `video_upload_success` | Video uploaded successfully | `video_id` (String)<br>`publisher_user_id` (String)<br>`is_game_enabled` (Boolean)<br>`game_type` (GameType)<br>`is_nsfw` (Boolean)<br>`type_ext` (VideoCreationType)<br>`affiliate` (String?) |
| `video_upload_error_shown` | When upload error is shown | `reason` (String)<br>`type_ext` (VideoCreationType)<br>`affiliate` (String?) |
| `video_upload_type_selected` | When user selects a video upload type (AI or manual) | `type_ext` (VideoCreationType) |
| `video_generation_model_selected` | When user selects an AI video generation model | `model` (String) |
| `create_ai_video_clicked` | When user clicks to create an AI-generated video | `model` (String)<br>`prompt` (String) |
| `ai_video_generated` | When AI video generation completes (success or failure) | `model` (String)<br>`prompt` (String)<br>`is_success` (Boolean)<br>`reason` (String?)<br>`reason_type` (AiVideoGenFailureType?) |

**VideoCreationType**: `ai_video`, `upload_video`

**AiVideoGenFailureType**: `trigger_failed`, `generation_failed`

---

## Profile

| Event Name | Description | Properties |
|---|---|---|
| `profile_page_viewed` | When user lands on profile page or a creator's profile | `total_videos` (Int)<br>`is_own_profile` (Boolean)<br>`publisher_user_id` (String) |
| `edit_profile_started` | User opens edit profile screen | `source` (EditProfileSource) |
| `edit_profile_completed` | User clicks on save changes | `username_updated` (Boolean)<br>`profile_image_updated` (Boolean)<br>`bio_updated` (Boolean) |
| `edit_profile_cancelled` | User exits without saving | — |
| `upload_video_clicked` | When user clicks on upload video CTA | `page_name` (String) |

**EditProfileSource**: `settings`, `profile`

---

## Notifications

| Event Name | Description | Properties |
|---|---|---|
| `enable_push_notification_popup_shown` | When the push notification permission popup is shown | `source` (AnalyticsAlertsRequestType) |
| `notifications_enabled` | When user enables push notifications | `source` (AnalyticsAlertsRequestType) |

**AnalyticsAlertsRequestType**: `follow_back`, `video`, `default`, `tournament`

---

## Wallet

| Event Name | Description | Properties |
|---|---|---|
| `wallet_page_viewed` | When user lands on the wallet page and wallet gets loaded | — |
| `cents_to_dolr_converted` | Tapping on Withdraw Now after updating withdraw amount in Wallet for Cents to DOLR flow | `cents_converted` (Double) |
| `third_party_wallet_transferred` | Tapping on Send icon in Wallet transfer screen | `token_transferred` (Double) |
| `sats_to_btc_converted` | Tapping on Withdraw Now after updating withdraw amount in Wallet for SATs to BTC flow | `sats_converted` (Double) |
| `video_views_rewards_nudge_shown` | When BTC rewards nudge is shown to the user based on video views | `video_id` (String?)<br>`current_views` (Long?)<br>`reward_amount_btc` (Double?) |
| `how_to_earn_clicked` | When user clicks on "How to earn" in wallet section | — |
| `airdrop_claimed` | On airdrop claim attempt (both success and failure) | `token_type` (TokenType)<br>`is_success` (Boolean)<br>`claimed_amount` (Int)<br>`is_auto_credited` (Boolean) |

---

## Referral

| Event Name | Description | Properties |
|---|---|---|
| `referral_received` | When a referral attribution is received from an install referrer | `source` (String?)<br>`medium` (String?)<br>`campaign` (String?)<br>`term` (String?)<br>`content` (String?) |
| `attribution_failed` | When referral attribution fails | `reason` (String)<br>`error_code` (Int?)<br>`raw_referrer` (String?)<br>`processors_checked` (List\<String\>?)<br>`is_enterprise_device` (Boolean?)<br>`has_work_profile` (Boolean?) |
| `refer_and_earn_page_viewed` | When user lands on refer page | `earned_amount` (Double) |
| `referral_history_viewed` | When user clicks on referral history | `earned_amount` (Double) |
| `share_invites_clicked` | When user clicks on share invites | `referral_bonus` (Double) |

---

## Share & Follow

| Event Name | Description | Properties |
|---|---|---|
| `video_share_clicked` | When user clicks the share button on a video | `video_id` (String)<br>`source_screen` (SourceScreen)<br>`is_owner` (Boolean) |
| `share_app_opened_from_link` | When user opens the app from a shared link | `video_id` (String) |
| `user_followed` | When user clicks on follow icon on feed or in profile page | `publisher_user_id` (String)<br>`source` (SourceScreen)<br>`cta_type` (CtaType) |
| `user_unfollowed` | When user clicks on un-follow icon on feed or profile | `publisher_user_id` (String)<br>`source` (SourceScreen)<br>`cta_type` (CtaType) |
| `followers_list_viewed` | When user clicks to check followers/following list | `publisher_user_id` (String)<br>`total_count` (Long)<br>`tab` (FollowersListTab) |

**SourceScreen**: `homefeed`, `profile`

**FollowersListTab**: `following`, `followers`

---

## Leaderboard

| Event Name | Description | Properties |
|---|---|---|
| `leaderboard_page_viewed` | When user lands on leaderboard | `leaderboard_tab` (LeaderBoardTabType) |
| `leaderboard_page_loaded` | When leaderboard data finishes loading | `leaderboard_tab` (LeaderBoardTabType)<br>`rank` (Int)<br>`visible_rows` (Int?) |
| `leaderboard_tab_clicked` | When user clicks on a leaderboard tab | `leaderboard_tab` (LeaderBoardTabType) |
| `leaderboard_calendar_clicked` | When user clicks the calendar icon on leaderboard | `leaderboard_tab` (LeaderBoardTabType)<br>`rank` (Int) |
| `leaderboard_day_selected` | When user selects a specific day on leaderboard calendar | `day` (Int)<br>`date` (String)<br>`rank` (Int)<br>`visible_rows` (Int?) |

**LeaderBoardTabType**: `daily`, `all`

---

## AI Chatbot

| Event Name | Description | Properties |
|---|---|---|
| `influencer_cards_viewed` | Influencer selection screen is shown | `influencers_shown` (List\<String\>)<br>`total_cards` (Int) |
| `influencer_card_clicked` | User clicks on an influencer card | `influencer_id` (String)<br>`influencer_type` (String)<br>`click_type` (InfluencerClickType)<br>`position` (Int) |
| `chat_influencer_clicked` | User clicks Talk from profile or card | `influencer_id` (String)<br>`influencer_type` (String)<br>`source` (InfluencerSource) |
| `chat_session_started` | Chat screen is opened with influencer | `influencer_id` (String)<br>`influencer_type` (String)<br>`chat_session_id` (String)<br>`source` (InfluencerSource) |
| `user_message_sent` | User sends a message in chat | `influencer_id` (String)<br>`influencer_type` (String)<br>`chat_session_id` (String)<br>`message_length` (Int)<br>`message_type` (String)<br>`message` (String) |
| `ai_message_delivered` | AI sends a response to user | `influencer_id` (String)<br>`influencer_type` (String)<br>`chat_session_id` (String)<br>`response_latency_ms` (Int)<br>`response_length` (Int)<br>`message` (String) |

**InfluencerClickType**: `talk`, `view_profile`

**InfluencerSource**: `card`, `profile`

---

## Create Bot

| Event Name | Description | Properties |
|---|---|---|
| `create_bot_cta_clicked` | User taps on "Create Bot" entry point | `source` (BotCreationSource) |
| `bot_creation_started` | User enters 3-step creation flow | `source` (BotCreationSource) |
| `bot_description_submitted` | User completes Step 1 (Describe your bot) | `description_text` (String)<br>`source` (BotCreationSource) |
| `bot_description_accepted` | User accepts generated description (Step 2) | `description_edited` (Boolean)<br>`description_text` (String)<br>`source` (BotCreationSource) |
| `bot_profile_generated` | System generates bot identity (Step 3 screen) | `name_generated` (String)<br>`avatar_generated` (Boolean)<br>`source` (BotCreationSource) |
| `create_bot_clicked` | User taps final "Create Bot" button | `retries` (Int)<br>`source` (BotCreationSource) |
| `bot_creation_success` | Bot successfully created | `bot_id` (String)<br>`source` (BotCreationSource) |
| `bot_creation_failed` | Bot creation failed | `error_code` (String)<br>`error_stage` (BotCreationErrorStage)<br>`retry_available` (Boolean)<br>`source` (BotCreationSource) |

**BotCreationSource**: `chat_page`, `profile_page`

**BotCreationErrorStage**: `user_description`, `asset_generation`, `final_create`

---

## Tournament

| Event Name | Description | Properties |
|---|---|---|
| `tournament_screen_viewed` | User opens tournament screen | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`session_id` (String) |
| `tournament_registration_initiated` | User clicks Register | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`entry_fee_points` (Int)<br>`user_point_balance` (Int)<br>`tournament_duration` (Int)<br>`session_id` (String) |
| `tournament_registered` | User successfully registers | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`entry_fee_points` (Int?)<br>`entry_fee_credits` (Int?)<br>`registration_time` (String)<br>`session_id` (String) |
| `tournament_state_changed` | Tournament participation state changes (e.g., Join CTA activated) | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`from_state` (TournamentState)<br>`to_state` (TournamentState)<br>`tokens_required` (Int?)<br>`user_diamonds` (Int?)<br>`session_id` (String) |
| `tournament_joined` | User joins tournament | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`join_time` (String)<br>`diamonds_allocated` (Int)<br>`session_id` (String) |
| `tournament_answer_submitted` | User answers a video in the tournament | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`answer_result` (TournamentAnswerResult)<br>`score_delta` (Int)<br>`diamonds_remaining` (Int)<br>`session_id` (String)<br>`emoji_shown` (List\<String\>)<br>`user_response` (String)<br>`ai_response` (String) |
| `tournament_exit_attempted` | User presses back during tournament | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`diamonds_remaining` (Int)<br>`session_id` (String) |
| `tournament_exit_nudge_shown` | Exit warning modal shown | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`nudge_type` (String)<br>`session_id` (String) |
| `tournament_exit_confirmed` | User exits tournament | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`diamonds_remaining` (Int)<br>`session_id` (String) |
| `tournament_out_of_diamonds_shown` | User runs out of diamonds | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`diamonds_remaining` (Int)<br>`session_id` (String) |
| `tournament_ended` | Tournament duration ends | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`tournament_name` (String)<br>`session_id` (String) |
| `tournament_result_screen_viewed` | Win/Lose screen shown | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`result` (TournamentResult)<br>`final_score` (Int)<br>`rank` (Int)<br>`session_id` (String) |
| `tournament_leaderboard_viewed` | User views tournament leaderboard | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`user_rank` (Int)<br>`is_winner` (Boolean)<br>`session_id` (String) |
| `tournament_reward_earned` | User wins prize | `tournament_id` (String)<br>`tournament_type` (AnalyticsTournamentType)<br>`reward_amount_inr` (Int)<br>`reward_currency` (String)<br>`rank` (Int) |

**AnalyticsTournamentType**: `smiley`, `hot_or_not`

**TournamentState**: `registration_required`, `registered`, `join_now`, `join_now_with_tokens`, `join_now_with_credit`, `join_now_disabled`, `ended`

**TournamentAnswerResult**: `right`, `wrong`

**TournamentResult**: `win`, `lose`

---

## Subscription

| Event Name | Description | Properties |
|---|---|---|
| `pro_nudge_impression` | When Pro subscription nudge is shown to the user | `entry_point` (SubscriptionEntryPoint) |
| `pro_nudge_clicked` | When user clicks on the Pro subscription nudge | `entry_point` (SubscriptionEntryPoint) |
| `pro_plan_viewed` | When user views the Pro plan details page | `entry_point` (SubscriptionEntryPoint)<br>`plan_price` (Double)<br>`credits_offered` (Int) |
| `pro_buy_clicked` | When user clicks the buy button on the Pro plan | `plan_price` (Double)<br>`payment_provider` (PaymentProvider) |
| `pro_payment_result` | When the Pro payment completes (success or failure) | `payment_status` (PaymentStatus)<br>`amount_paid` (Double?)<br>`currency` (String?)<br>`transaction_id` (String?) |
| `pro_status_updated` | When user's Pro subscription status changes | `pro_status` (Boolean)<br>`credits_granted` (Int)<br>`source` (ProStatusSource) |
| `credits_consumed` | When Pro credits are consumed for a feature | `feature` (CreditFeature)<br>`credits_used` (Int)<br>`credits_remaining` (Int) |
| `credits_exhausted` | When user runs out of Pro credits | `last_used_feature` (CreditFeature) |

**SubscriptionEntryPoint**: `home_feed`, `profile`, `hamburger`, `ai_video`, `ai_chatbot`, `tournament`

**PaymentProvider**: `apple`, `google`

**PaymentStatus**: `success`, `failure`

**ProStatusSource**: `purchase`, `renewal`

**CreditFeature**: `ai_video`, `tournament`, `chatbot`
