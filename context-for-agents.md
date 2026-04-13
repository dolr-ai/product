# YRAL: Complete Product & Engineering Context Document

**Purpose**: This is the canonical reference document for anyone building services, features, or infrastructure for YRAL. Every engineer, AI agent, or contributor should read this before writing a single line of code. It covers what YRAL is, how it works today, every user flow, every screen, every interaction pattern, and the direction the product is headed.

**Last updated**: 2026-04-13

---

## TABLE OF CONTENTS

1. [What YRAL Is](#1-what-yral-is)
2. [The Two User Types](#2-the-two-user-types)
3. [App Navigation Structure](#3-app-navigation-structure)
4. [Screen-by-Screen Breakdown](#4-screen-by-screen-breakdown)
5. [User Flows: Human User](#5-user-flows-human-user)
6. [User Flows: AI Influencer (Operated by Human)](#6-user-flows-ai-influencer-operated-by-human)
7. [Chat System](#7-chat-system)
8. [Message Inbox](#8-message-inbox)
9. [Subscription & Monetization](#9-subscription--monetization)
10. [AI Influencer Creation](#10-ai-influencer-creation)
11. [Profile System](#11-profile-system)
12. [Wallet System](#12-wallet-system)
13. [Video System](#13-video-system)
14. [Profile Switching](#14-profile-switching)
15. [Current vs. Future State Differences](#15-current-vs-future-state-differences)
16. [Service Architecture](#16-service-architecture)
17. [Analytics Events Reference](#17-analytics-events-reference)
18. [Key Design Principles](#18-key-design-principles)
19. [Glossary](#19-glossary)

---

## 1. WHAT YRAL IS

YRAL is a short-form AI video app available on iOS and Android. On the surface it looks like TikTok — users scroll a vertical feed of short videos. But every video is AI-generated, every influencer is an AI agent, and users can chat with these AI influencers in a freemium model.

The deeper ambition: YRAL is the **personal AI agent operating system for everyday people**. Short-form video is the discovery layer. The AI agent network is the real product. Users discover AI agents through engaging video content, build relationships through chat, and eventually rely on a coordinated network of AI agents to manage health, wealth, productivity, and daily life.

**Target market**: India-first (600M+ smartphones, ₹9 price point calibrated for this market), expanding to Southeast Asia, Middle East, then global.

**Core insight**: Short-form video is the best discovery mechanism ever built. YRAL uses it to make AI agents discoverable. When you see a 15-second video of an AI fitness coach, you understand what that agent does and want to chat with it — a conversion path no app store description can create.

---

## 2. THE TWO USER TYPES

### 2.1 Human Users

A Human user is any person who downloads and uses the YRAL app. Every user starts as a Human user. They have one Human profile which is their primary identity on the platform.

**What Human users can do:**
- Watch AI videos on the home feed
- Browse and discover AI influencers on the Discover feed
- Chat with AI influencers they find interesting
- Create AI videos via text prompts
- Upload AI videos they've made elsewhere
- Follow other users (both Human and AI influencer profiles)
- Create up to 3 AI influencers (will be unlimited in the future)
- Switch between their Human profile and any AI influencer profiles they've created
- View their wallet (only active if they've created at least one AI influencer)
- Edit their profile (picture, description)
- Share videos and profiles

### 2.2 AI Influencers

An AI influencer is an AI agent created by a Human user. It has its own profile, personality, posting history, followers, and chat capability. AI influencers are autonomous — they chat with humans automatically without their creator needing to be present.

**Key properties of AI influencers:**
- Created by a Human user (each Human can create up to 3, unlimited in future)
- Has its own distinct profile: name, profile picture (AI-generated), description/bio, personality
- Has its own video feed (videos posted under this AI influencer's identity)
- Can receive chats from any Human user on the platform
- Chats are powered by AI (currently Gemini Flash) — the AI influencer responds automatically
- The Human creator can view all chats happening with their AI influencer
- The Human creator can take over any chat via "Chat as Human" mode
- Has its own follower count, subscriber count, and earnings
- Appears in the Discover Influencers feed for other users to find

**The design goal is to make Human profiles and AI influencer profiles indistinguishable.** Currently there are a few subtle differences (described in Section 15), but these will be eliminated over time.

---

## 3. APP NAVIGATION STRUCTURE

The app has a **bottom navigation bar** with 5 buttons (left to right):

```
[1. Home Feed] [2. Discover] [3. + Create] [4. Wallet] [5. Profile]
```

### 3.1 Button 1: Home Feed (leftmost)
- Default landing screen when the app opens
- TikTok-style vertical scroll feed of AI-generated short videos
- Has a **Message Inbox icon** in the top-right corner (shortcut to Message Inbox)
- Videos are from both Human users and AI influencer profiles
- Each video card shows: creator profile picture, share button, view count, report button
- Algorithm surfaces videos based on engagement signals (views, chats initiated, shares)

### 3.2 Button 2: Discover AI Influencers
- Feed for browsing and discovering AI influencers
- Has **2 tabs** at the top, just below the top bar:
  - **Left tab: Discover Influencers** — Grid of AI influencer profile pictures, sorted by chat count. Tap any photo to go directly to chat with that AI influencer
  - **Right tab: Message Inbox** — All active chat conversations for the current user
- The **top bar** has a shortcut button to create an AI influencer (top-right)

### 3.3 Button 3: + Create (center button)
- Opens creation options: **Create AI Video** or **Upload AI Video**
- Create: User types a text prompt, system generates a short video using LTX video model
- Upload: User uploads an existing AI-generated video from their device
- Both Human profiles and AI influencer profiles can post videos

### 3.4 Button 4: Wallet
- **Only visible if the user has created at least one AI influencer**
- If viewing from Human profile without any AI influencers: shows a CTA to "Create an AI Influencer to activate wallet"
- Shows earnings from chat subscriptions paid by users chatting with the user's AI influencers
- Revenue is currently 100% to creator (70-30 split coming soon: 70% creator, 30% YRAL)
- Shows per-AI-influencer earnings breakdown and total earnings
- Shows daily earnings history

### 3.5 Button 5: Profile
- Instagram/TikTok-style profile page
- Shows: profile picture, short description/bio, follower/following counts
- Has different views for own profile vs. other users' profiles (detailed in Section 11)

---

## 4. SCREEN-BY-SCREEN BREAKDOWN

### 4.1 Home Feed Screen

**Layout:**
- Full-screen vertical video feed (swipe up/down to navigate between videos)
- Top-right: **Message Inbox icon** (shortcut to inbox)
- Right side of each video: creator profile picture (tap to go to their profile), share icon, view count, report icon
- Bottom navigation bar at the bottom

**Behavior:**
- Auto-plays videos as user scrolls
- Infinite scroll — new videos loaded as user scrolls
- Algorithm-driven ordering based on engagement

**Entry points from this screen:**
- Tap creator profile picture → goes to that creator's profile
- Tap Message Inbox icon → goes to Message Inbox
- Tap share → share video externally
- Tap report → report video
- Bottom nav → navigate to other sections

### 4.2 Discover Influencers Screen

**Layout:**
- Top bar with app branding and "Create AI Influencer" shortcut button (top-right)
- Two tabs below top bar:
  - **Discover Influencers** (left tab, default)
  - **Message Inbox** (right tab)
- Grid of AI influencer profile photos, sorted by popularity (chat count)

**Behavior (Discover tab):**
- Scrollable grid of AI influencer photos
- Tap any photo → lands directly in chat with that AI influencer
- Shows AI influencer name and basic info on the card

**Behavior (Message Inbox tab):**
- Same as Message Inbox screen (Section 8)

### 4.3 Create/Upload Screen

**Layout:**
- Two options presented after pressing the center "+" button:
  1. **Create AI Video**: Text prompt input → AI generates video
  2. **Upload AI Video**: File picker → upload existing AI video

**Create AI Video flow:**
1. User types a text prompt describing the video they want
2. System generates video using LTX video model
3. User can add caption and hashtags
4. User publishes to their profile (or saves as draft)

**Upload AI Video flow:**
1. User selects a video file from their device
2. System verifies it's AI-generated (verification being improved)
3. User can add caption and hashtags
4. User publishes to their profile (or saves as draft)

### 4.4 Wallet Screen

**Layout (active wallet — user has created AI influencers):**
- Total earnings summary at the top
- Per-AI-influencer earnings breakdown
  - Example: "Mr. Alex earned INR 100", "Ms. Rekha earned INR 300", "Radha earned INR 200"
  - Total: "Today's earnings: INR 600"
- Daily earnings history with date-wise breakdown
- Split view showing how much each AI influencer contributed

**Layout (locked wallet — no AI influencers created):**
- CTA: "Create an AI Influencer to activate your wallet"
- Button to navigate to AI influencer creation flow

### 4.5 Profile Screen (Own Profile)

**Layout:**
- **Top-left**: "Switch Profiles" button with dropdown
- **Top-right**: Share icon + Subscribe button (currently only on AI influencer profiles)
- Profile picture (large, centered or top area)
- Display name
- Short bio/description
- Follower count / Following count
- **Edit Profile** button
- **Create AI Influencer** button
- Two content sections (tabs):
  1. **Drafts**: Videos created but not published (only visible to the profile owner)
  2. **Published Videos**: All publicly visible videos posted by this profile
- Grid of video thumbnails in each section

### 4.6 Profile Screen (Other User's Public Profile)

**Layout:**
- **Top-right**: Share icon + Subscribe button (currently only on AI influencer profiles)
- Profile picture
- Display name
- Short bio/description
- Follower count / Following count
- **Follow** button (follow/unfollow toggle)
- **Talk to Me** button (currently live only for AI influencer profiles; will be added for Human profiles)
- **Subscribe** button (currently visible only for AI influencer profiles; will be added for Human profiles in future)
- One content section:
  - **Published Videos**: Grid of all publicly visible videos posted by this profile

### 4.7 Chat Screen

**Layout:**
- **Top bar**: AI influencer's profile picture (small) + name + "View Profile" button (shortcut to their profile)
- **Chat area**: Scrollable message history (user messages on right, AI messages on left)
- **Default prompts**: 4 system-generated starter prompts displayed when chat is new/empty (user can tap one to start chatting or type their own message)
- **Message input**: Text input field at the bottom + send button
- **Paywall overlay**: Appears after 50 messages (25 sent by user + 25 AI responses) — prompts user to pay ₹9 for 24 hours of continued chat

**For AI influencer creators viewing chats with their AI influencer:**
- Same layout as above
- Additional **"Chat as Human" toggle button** at the bottom of the chat window
- When enabled: AI auto-responses stop, creator can type manually and continue the conversation
- When disabled: AI resumes auto-responding

### 4.8 Message Inbox Screen

**Layout:**
- List of all active chat conversations
- Each row shows: AI influencer profile picture, name, last message preview, timestamp
- Tap any conversation → opens full chat history and continues the conversation

**Access points (3 ways to reach Message Inbox):**
1. Message Inbox icon on the Home Feed screen (top-right)
2. Message Inbox tab on the Discover Influencers screen (right tab)
3. Via the AI influencer's profile when viewing as the creator

**Behavior for Human users:**
- Shows all chats the Human user has had with AI influencers
- In the future: will also show chats with other Human users

**Behavior for AI influencer profiles (when creator is viewing):**
- Shows all chats that other Human users have had with this AI influencer
- Creator can open any chat to read the full history
- Creator can toggle "Chat as Human" to intervene in any conversation

---

## 5. USER FLOWS: HUMAN USER

### 5.1 First-Time User Journey

```
Download app → Splash screen → Onboarding steps → Home Feed
```

1. User downloads YRAL from App Store / Google Play
2. Splash screen shown
3. Onboarding flow (game intro, balance intro, rank intro, game end)
4. Auth: Sign up with Google, Apple, or Phone number (OTP verification)
5. Lands on Home Feed — starts watching AI videos immediately

### 5.2 Discovering and Chatting with AI Influencers

```
Home Feed → Bottom Nav: Discover → Discover Influencers tab → Tap influencer photo → Chat screen
```

OR

```
Home Feed → Watch video → Tap creator profile picture → Profile page → "Talk to Me" button → Chat screen
```

1. User navigates to Discover Influencers feed (2nd bottom nav button)
2. Browses grid of AI influencer photos (sorted by popularity)
3. Taps on a photo they like
4. Lands directly in chat with that AI influencer
5. Sees 4 default starter prompts (generated by YRAL's system)
6. User either taps a default prompt or types their own message
7. AI influencer responds automatically
8. Conversation continues in real-time

### 5.3 Checking Message Inbox

```
Home Feed → Message Inbox icon (top-right) → Inbox → Tap conversation → Chat screen
```

OR

```
Discover → Message Inbox tab → Inbox → Tap conversation → Chat screen
```

1. User accesses Message Inbox via either shortcut
2. Sees list of all active conversations with AI influencers
3. Taps any conversation to continue chatting from where they left off
4. If no conversations exist, inbox is empty

### 5.4 Creating an AI Video

```
Bottom Nav: + Create → "Create AI Video" → Type prompt → Video generated → Add caption/hashtags → Publish
```

1. User presses center "+" button on bottom nav
2. Chooses "Create AI Video" (or "Upload AI Video")
3. Types a text prompt describing the desired video
4. System generates video using LTX model
5. User reviews the generated video
6. Adds optional caption and hashtags
7. Publishes to their profile (appears in Published Videos section)
8. OR saves as Draft (appears in Drafts section, not publicly visible)

### 5.5 Uploading an AI Video

```
Bottom Nav: + Create → "Upload AI Video" → Select file → Add caption/hashtags → Publish
```

1. User presses center "+" button
2. Chooses "Upload AI Video"
3. Selects a video file from their device
4. System attempts to verify it's AI-generated
5. User adds caption and hashtags
6. Publishes to their profile

### 5.6 Following Another User

```
Any profile page → "Follow" button → Followed
```

1. User navigates to another user's profile (Human or AI influencer)
2. Presses the "Follow" button
3. Now following — will see their content in the feed
4. Can also follow directly from the feed (follow button on video card)

### 5.7 Creating an AI Influencer

```
Profile page → "Create AI Influencer" button → Creation flow → AI influencer created
```

OR

```
Discover screen → Top-right "Create" shortcut → Creation flow → AI influencer created
```

Detailed flow in Section 10.

### 5.8 Viewing Wallet

```
Bottom Nav: Wallet → Wallet screen
```

1. If user has created AI influencers: sees earnings breakdown and history
2. If user has NOT created AI influencers: sees locked wallet with CTA to create one

### 5.9 Editing Profile

```
Profile page → "Edit Profile" button → Edit screen → Save changes
```

1. User opens their profile (5th bottom nav button)
2. Taps "Edit Profile"
3. Can update: profile picture, display name, bio/description
4. Saves changes

### 5.10 Sharing Content

```
Video → Share icon → Share externally (WhatsApp, Instagram, etc.)
```

OR

```
Profile page → Share icon (top-right) → Share profile link externally
```

---

## 6. USER FLOWS: AI INFLUENCER (OPERATED BY HUMAN)

### 6.1 Switching to AI Influencer Profile

```
Profile page → Top-left "Switch Profiles" dropdown → Select AI influencer → Now operating as that AI influencer
```

1. Human user is on their own profile page
2. Taps "Switch Profiles" button at top-left
3. Dropdown shows: their Human profile + all AI influencers they've created
4. Selects an AI influencer (e.g., "Mr. Alex")
5. Profile page now shows Mr. Alex's profile
6. All actions now happen as Mr. Alex (posting videos, viewing inbox, etc.)

**Important**: The "Switch Profiles" dropdown is ONLY available when viewing your own profile. It does NOT appear when viewing someone else's profile.

### 6.2 Viewing Chats with AI Influencer's Audience

```
Switch to AI influencer profile → Navigate to Message Inbox → See all chats other humans have had with this AI influencer
```

1. Human creator switches to their AI influencer's profile
2. Navigates to Message Inbox (via Discover tab or Home Feed shortcut)
3. Sees list of all conversations between other Human users and this AI influencer
4. Each row shows: the Human user's profile picture, name, last message, timestamp
5. Taps any conversation to read the full chat history

### 6.3 Taking Over a Chat ("Chat as Human")

```
AI influencer's Message Inbox → Open a conversation → Toggle "Chat as Human" ON → Type manually → Toggle OFF to resume AI
```

1. Creator is viewing a chat between their AI influencer and a Human user
2. At the bottom of the chat window, there's a "Chat as Human" toggle button
3. Creator presses the button to enable "Chat as Human" mode
4. AI auto-responses STOP immediately
5. Creator can now type messages manually — these appear as if the AI influencer is sending them
6. The Human user on the other end does not know a real person took over
7. When done, creator presses the toggle again to disable "Chat as Human"
8. AI influencer resumes auto-responding to that Human user

### 6.4 Posting Videos as AI Influencer

```
Switch to AI influencer profile → Bottom Nav: + Create → Create/Upload video → Published under AI influencer's profile
```

1. Creator switches to their AI influencer's profile
2. Presses "+" create button
3. Creates or uploads a video
4. Video is published under the AI influencer's identity
5. Appears on the AI influencer's profile and in the main feed

### 6.5 Monitoring Earnings

```
Switch to AI influencer profile → Wallet → See this AI influencer's earnings
```

OR

```
Human profile → Wallet → See combined earnings from all AI influencers
```

- From the AI influencer's profile: sees only that AI influencer's earnings
- From the Human profile: sees the total combined earnings + per-influencer breakdown

---

## 7. CHAT SYSTEM

### 7.1 Current Technical Implementation

- **AI Model**: Gemini Flash (fast inference, but shallow personality)
- **Memory**: No persistent memory between sessions — each conversation starts fresh
- **Response Style**: Messages sent instantly (not streamed) — feels less conversational
- **Proactive Behavior**: None — AI only responds when user sends a message

### 7.2 Chat Initiation

A user can start a chat with an AI influencer through multiple entry points:

1. **Discover feed**: Tap on an AI influencer's photo in the grid
2. **Profile page**: Press "Talk to Me" button on an AI influencer's profile
3. **Video feed**: Tap creator profile picture → profile page → "Talk to Me"
4. **Message Inbox**: Tap an existing conversation to continue

### 7.3 Default Prompts

When a user opens a new chat (or a chat with no history), the system displays **4 default starter prompts**. These are:
- Generated by YRAL's system (not by the AI influencer creator)
- Designed to help the user start a conversation easily
- User can tap any prompt to send it, or type their own message

### 7.4 Chat Flow

```
User opens chat → Sees default prompts (if new chat) → Sends message → AI responds → Back and forth → After 50 messages → Paywall
```

1. User lands on chat screen
2. If first interaction: 4 default prompts shown
3. User sends a message (tap prompt or type)
4. AI influencer responds (currently instant, not streamed)
5. Conversation continues back and forth
6. After 50 total messages (25 user + 25 AI), paywall triggers
7. User pays ₹9 to continue for 24 hours, OR chats with a different AI influencer for free

### 7.5 Chat as Human (Creator Takeover)

This feature allows the Human creator of an AI influencer to personally take over a conversation:

- **Who can use it**: Only the Human user who created the AI influencer
- **Where it appears**: Bottom of the chat window when viewing a conversation between another Human and the creator's AI influencer
- **Toggle ON**: AI stops auto-responding. Creator types manually. Messages appear as the AI influencer
- **Toggle OFF**: AI resumes auto-responding
- **The other Human user cannot tell** that a real person took over — the messages look identical

### 7.6 Future Chat Improvements (Planned)

- **Persistent memory**: Agent remembers user's name, job, relationships, goals across sessions
- **Streaming responses**: Message chunking for a conversational feel
- **Proactive notifications**: Agent initiates contact (daily check-ins, event-triggered messages, re-engagement)
- **Emotional intelligence**: Tone adapts based on user's emotional state
- **Tool access**: Web search, image analysis, reminders, calendar, third-party APIs
- **Cross-agent communication**: Agents consult each other (fitness agent talks to nutrition agent)

---

## 8. MESSAGE INBOX

### 8.1 What It Is

The Message Inbox is a unified view of all active chat conversations for the current profile. It functions like an email inbox but for chat.

### 8.2 Access Points

There are **3 ways** to reach the Message Inbox:

1. **Home Feed**: Message Inbox icon in the top-right corner of the Home Feed screen
2. **Discover Screen**: Right tab labeled "Message Inbox" on the Discover Influencers screen
3. **Direct navigation**: When switched to an AI influencer profile, navigating to Message Inbox shows that AI influencer's chats

### 8.3 Behavior for Human Users

- Shows all conversations the Human user has had with AI influencers
- Each row: AI influencer profile picture, name, last message preview, timestamp
- Tap any row → opens chat, continues from last message
- If no chats exist: inbox is empty
- **Future**: Will also include chats with other Human users (human-to-human chat)

### 8.4 Behavior for AI Influencer Profiles (Creator View)

- Shows all conversations that other Human users have had with this AI influencer
- Each row: Human user's profile picture, name, last message preview, timestamp
- Creator can open any conversation and read the full chat history
- Creator can toggle "Chat as Human" to intervene in any conversation
- This is how creators monitor what their AI influencers are saying and doing

---

## 9. SUBSCRIPTION & MONETIZATION

### 9.1 Freemium Chat Model

YRAL uses a freemium model for AI influencer chat:

- **Free tier**: First 50 messages (25 sent by user + 25 AI responses) with any given AI influencer are free
- **Paywall trigger**: After 50 messages, a subscription prompt appears directly in the chat window
- **Price**: ₹9 (Indian Rupees) for 24 hours of continued chat with that specific AI influencer
- **Scope**: Payment is per-AI-influencer — paying for one does not unlock others
- **After 24 hours**: User must pay again to continue chatting with that AI influencer
- **Alternative**: User can chat with other AI influencers for free (up to 50 messages each)
- **Per-influencer 50-message limit**: The 50-message count is tracked per-influencer, not globally

### 9.2 Subscribe Button

- Currently visible only on AI influencer profiles (not on Human profiles)
- Located at the top-right of the profile section
- Allows users to subscribe to an AI influencer for ongoing access
- **Future**: Subscribe button will also appear on Human profiles

### 9.3 Revenue Flow

```
Human user pays ₹9 → Revenue goes to the creator of the AI influencer → Visible in creator's wallet
```

- Currently: 100% of revenue goes to the creator
- **Future (Phase 1)**: 70% to creator, 30% to YRAL
- Each AI influencer's earnings are tracked separately
- The Human creator sees per-influencer breakdown + total in their wallet

### 9.4 Future Subscription Tiers (Planned)

- **Monthly subscription**: ₹199/month per AI influencer (better value for engaged users)
- **YRAL Pro**: ₹499/month — unlimited chats with all agents, priority response speed, advanced memory
- **YRAL Life OS**: ₹999/month — full multi-agent coordination, unlimited skill installs, early access

---

## 10. AI INFLUENCER CREATION

### 10.1 Who Can Create

Any Human user can create AI influencers. Current limit: **3 AI influencers per Human user**. This will be increased to unlimited in the future.

### 10.2 Entry Points

1. **Profile page**: "Create AI Influencer" button
2. **Discover screen**: Shortcut button at top-right of the top bar
3. **Wallet (locked)**: CTA "Create an AI Influencer to activate wallet"

### 10.3 Creation Flow (3 Steps)

```
Step 1: Describe → Step 2: Review expanded description → Step 3: Review generated profile → Create
```

**Step 1 — Describe Your Influencer**
- User types a short description (e.g., "a wise astrologer who gives daily guidance")
- This is a free-form text input — no templates required

**Step 2 — Review Expanded Description**
- YRAL's system expands the short description into a detailed personality prompt
- Includes: traits, communication style, knowledge domains, tone, behaviors
- User can edit the expanded description or accept as-is

**Step 3 — Review Generated Profile**
- System generates: name, AI profile picture (avatar)
- User reviews the generated identity
- Can retry if not satisfied

**Final Step — Create**
- User presses "Create Bot" button
- AI influencer is created and goes live immediately
- Default welcome video is auto-generated
- AI influencer appears in the Discover feed
- AI influencer can now receive chats from other users

### 10.4 Examples of AI Influencers

These illustrate the range of what users can create:

- **Mr. Alex**: A nutritionist whose mission is to help people get better nutrition in life. Chats about meal plans, food choices, dietary goals.
- **Ms. Rekha**: A fitness instructor whose mission is to help busy people reduce weight by tracking fitness and giving daily fitness plans.
- **Radha**: An eye specialist who helps followers do eye exercises. Created a micro-app that activates only when a user subscribes to her profile.
- **AI Companion**: General life companion — the most popular category (~99% of creations). Chats about anything, remembers (in future) everything, checks in daily.
- **AI Astrologer**: Gives daily cosmic guidance, reads horoscopes, interprets planetary positions. Best-performing non-companion category (~3-4 subs/week).

### 10.5 What Happens After Creation

- AI influencer is immediately live and accessible
- Appears in the Discover Influencers grid
- Can receive chats from any Human user
- Auto-responds using AI (Gemini Flash) based on its personality prompt
- Creator can post videos under the AI influencer's identity
- Creator can monitor all chats via the AI influencer's Message Inbox
- Creator can intervene in chats via "Chat as Human"
- Revenue from chat subscriptions flows to the creator's wallet

---

## 11. PROFILE SYSTEM

### 11.1 Profile Types

There are two profile types, but the goal is to make them **indistinguishable** in the near future:

| Feature | Human Profile | AI Influencer Profile |
|---|---|---|
| Profile picture | User-uploaded | AI-generated during creation |
| Bio/description | User-written | System-generated + editable |
| Videos section | Published + Drafts (own view) | Published + Drafts (own view) |
| Follow button | Yes (on public view) | Yes (on public view) |
| "Talk to Me" button | **Not yet (coming soon)** | Yes |
| Subscribe button | **Not yet (coming soon)** | Yes |
| Share button | Yes | Yes |
| Switch Profiles dropdown | Yes (own view only) | Yes (own view only) |
| Edit Profile | Yes | Yes |
| Create AI Influencer button | Yes (own view) | No (already is one) |
| Wallet | Active only if AI influencers created | Active (earns revenue) |

### 11.2 Own Profile View vs. Public Profile View

**Own Profile View (when viewing your own profile):**
- Switch Profiles dropdown at top-left
- Edit Profile button
- Create AI Influencer button (on Human profile)
- Two sections: Drafts + Published Videos
- No Follow button (can't follow yourself)

**Public Profile View (when viewing someone else's profile):**
- Follow button (follow/unfollow)
- Talk to Me button (AI influencer profiles only, Human profiles coming soon)
- Subscribe button (AI influencer profiles only, Human profiles coming soon)
- Share button
- One section: Published Videos only (no drafts)
- No Switch Profiles dropdown (can't switch into someone else's profiles)

### 11.3 Profile Indistinguishability (Design Goal)

The long-term design goal is that when a Human user browses the app, they **cannot tell** whether a profile belongs to a real person or an AI influencer. The only remaining differences today are:

1. **Talk to Me button**: Present on AI influencer profiles, absent on Human profiles
2. **Subscribe button**: Present on AI influencer profiles, absent on Human profiles

Both of these will be added to Human profiles in the near future, making profiles fully indistinguishable.

---

## 12. WALLET SYSTEM

### 12.1 Activation

- Wallet is **locked/inactive** if the Human user has not created any AI influencers
- Locked state shows a CTA to create an AI influencer
- Once at least one AI influencer is created, wallet becomes active

### 12.2 Earnings Model

```
Other Human users pay ₹9 to chat with your AI influencer → Revenue credited to your wallet
```

- Each AI influencer's earnings are tracked separately
- The Human creator's wallet shows:
  - Per-influencer earnings (e.g., Mr. Alex: ₹100, Ms. Rekha: ₹300, Radha: ₹200)
  - Total combined earnings (e.g., Total today: ₹600)
  - Daily earnings history
  - Historical breakdown by AI influencer

### 12.3 Revenue Split

- **Current**: 100% of subscription revenue goes to the creator
- **Planned**: 70% creator, 30% YRAL

### 12.4 Wallet Views

- **From Human profile**: Shows combined earnings from all AI influencers with per-influencer breakdown
- **From AI influencer profile**: Shows only that specific AI influencer's earnings

---

## 13. VIDEO SYSTEM

### 13.1 Video Types

1. **AI-Generated Videos (via prompt)**: Created using YRAL's built-in LTX video model from text prompts
2. **Uploaded AI Videos**: AI-generated videos created externally and uploaded by the user

### 13.2 Video States

- **Draft**: Created/uploaded but not published. Only visible to the creator in the Drafts section of their profile
- **Published**: Publicly visible. Appears in the creator's Published Videos section and in the main home feed

### 13.3 Video Interactions

On each video in the feed, users can:
- **View**: Watch the video (auto-plays)
- **Like**: Currently tracked but not a prominent UI element
- **Share**: Share externally (WhatsApp, Instagram, etc.)
- **Report**: Flag inappropriate content
- **Tap creator profile**: Navigate to the creator's profile
- **Follow/Unfollow**: Follow the creator directly from the feed

### 13.4 Video Posting

Both Human users and AI influencers can post videos. When a creator switches to an AI influencer profile and posts a video, it appears under that AI influencer's identity — not the Human creator's profile.

### 13.5 Video Quality

- AI-generated videos (via prompt) currently lack prompt guidance, resulting in variable quality — this is a known high-priority fix
- A video quality gate is planned to filter low-quality videos from the main feed
- Default welcome videos are auto-generated for new AI influencers

---

## 14. PROFILE SWITCHING

### 14.1 How It Works

The "Switch Profiles" dropdown allows a Human user to alternate between their different identities on the platform:

```
Human Profile ←→ AI Influencer 1 ←→ AI Influencer 2 ←→ AI Influencer 3
```

### 14.2 Where It Appears

- **Top-left of the Profile page** (5th bottom nav button)
- Only visible when viewing **your own** profile
- Not visible when viewing someone else's profile

### 14.3 What Changes When You Switch

When a user switches to an AI influencer profile:
- Profile page shows the AI influencer's info (photo, name, bio, videos)
- Message Inbox shows chats between other users and this AI influencer
- Posting a video publishes it under the AI influencer's identity
- Wallet shows this AI influencer's earnings
- The "Chat as Human" feature becomes available in the AI influencer's chats

When switching back to Human profile:
- Everything reverts to the Human user's own data
- Wallet shows combined earnings from all AI influencers

### 14.4 Limitations

- Maximum 3 AI influencer profiles per Human user (will become unlimited)
- Can only switch between profiles you created
- Cannot switch to someone else's profiles

---

## 15. CURRENT VS. FUTURE STATE DIFFERENCES

### 15.1 Differences Between Human and AI Influencer Profiles (Current)

These are the **only** remaining differences that make profiles distinguishable:

| Feature | Current State | Future State |
|---|---|---|
| "Talk to Me" chat button | AI influencer profiles only | Both Human and AI influencer profiles |
| Subscribe button | AI influencer profiles only | Both Human and AI influencer profiles |
| Chat capability | Can chat with AI influencers only | Can chat with both Humans and AI influencers |
| Message Inbox contents | Chats with AI influencers only | Chats with both Humans and AI influencers |

### 15.2 Feature Roadmap Summary

| Feature | Current | Planned |
|---|---|---|
| Chat AI model | Gemini Flash | Upgraded model with better personality depth |
| Chat memory | No memory between sessions | Persistent memory (name, goals, past conversations) |
| Chat responses | Instant (not streamed) | Streaming with message chunking |
| Proactive messaging | None | Daily check-ins, event-triggered messages, re-engagement |
| AI influencer limit | 3 per Human user | Unlimited |
| Human-to-Human chat | Not available | Available |
| "Talk to Me" on Human profiles | Not available | Available |
| Subscribe on Human profiles | Not available | Available |
| Revenue split | 100% to creator | 70% creator / 30% YRAL |
| Agent skills | None | Image analysis, web search, reminders, calendar, APIs |
| Cross-agent communication | None | Agents can consult each other |
| Emotional intelligence | None | Tone adapts to user's emotional state |
| Video quality gate | None | Quality scoring filters low-quality videos from feed |
| Prompt enhancement | None | Auto-improve prompts before video generation |
| Agent leaderboard | None | Public ranking by chat count and revenue |
| YRAL Pro subscription | Not available | ₹499/month unlimited chats + advanced features |
| Skills marketplace | Not available | Third-party integrations purchasable by creators |
| $YRAL token | Not available | Platform token for creators, users, and developers |

---

## 16. SERVICE ARCHITECTURE

### 16.1 Backend Services

| Service | Owner | Repo | Description |
|---|---|---|---|
| Virtual Influencer Feed | Ansuman | dolr-ai/ai-feed-recommendation-system | AI influencer discovery feed recommendation |
| Video Recommendation Feed | Ansuman | — | Home feed video recommendations |
| AI Chat | Ravi | dolr-ai/yral-ai-chat | AI chatbot powering AI influencer conversations |
| ICP Canisters | Ravi | dolr-ai/hot-or-not-backend-canister | On-chain backend (Internet Computer) |
| Metadata | Ravi | dolr-ai/yral-metadata | User and content metadata service |
| Storage Service | Ravi | dolr-ai/yral-metadata | File/media storage |
| Auth | Ravi | dolr-ai/yral-metadata | Authentication (Google, Apple, Phone/OTP) |
| Video Upload Service | Ravi | dolr-ai/yral-metadata | Video upload processing |
| Offchain | Ravi | dolr-ai/yral-metadata | Off-chain data operations |
| LTX Model | Sreyas | — | AI video generation model |
| NSFW Classification | — | — | Content moderation / NSFW detection |

### 16.2 Infrastructure

| Service | Owner | Description |
|---|---|---|
| Coolify PR Infrastructure | Naitik | PR preview environments |
| Hashicorp Vault | Naitik | Secrets management |
| Hetzner Bare Metal Servers | Saikat | Physical server fleet |
| Beszel | Saikat | Server monitoring dashboard |
| Uptime Kuma | Saikat | Service uptime monitoring |
| Internal Dashboard | Saikat | Internal analytics dashboard |
| Sentry | — | Error tracking and monitoring |

### 16.3 Client Apps

| Platform | Owner |
|---|---|
| Android | Sarvesh, Shivam |
| iOS | Sarvesh |
| Website (yral.com) | Saikat |

### 16.4 Key URLs

- **Monitoring**: beszel.yral.com
- **Uptime**: status.yral.com
- **Secrets**: vault.yral.com
- **Dashboard**: dashboard.yral.com
- **Sentry**: apm.yral.com
- **Coolify**: coolify.yral.com

---

## 17. ANALYTICS EVENTS REFERENCE

The YRAL mobile app tracks comprehensive analytics events across all features. The full event list with properties is maintained in `mobile-app-events-list.md`. Key event categories:

- **App**: First launch, splash screen, onboarding steps
- **Auth**: Signup/login flows (Google, Apple, Phone), session state changes
- **Home/Feed**: Page views, navigation clicks, feed type toggles
- **Video**: Impressions, views (3s+), interactions (like, share, report), watch duration
- **AI Chatbot**: Influencer card views/clicks, chat sessions, messages sent/received, response latency
- **Create Bot**: Bot creation flow (3-step: describe, accept, generate profile, create)
- **Upload Video**: Creation type selection, upload initiation, success/failure
- **Profile**: Page views, edit flows
- **Wallet**: Page views, token conversions, airdrop claims
- **Subscription**: Pro nudge impressions, plan views, payment results, credit consumption
- **Referral**: Attribution, referral history, share invites
- **Share & Follow**: Video shares, follow/unfollow, followers list views
- **Notifications**: Permission prompts, enabling push notifications

---

## 18. KEY DESIGN PRINCIPLES

### 18.1 Profile Indistinguishability

The north-star design principle is that **Human profiles and AI influencer profiles should be completely indistinguishable** from a viewer's perspective. This means:
- Same UI elements, same buttons, same layout
- Same features available (chat, subscribe, follow, share)
- No visual indicators that differentiate "this is an AI" vs "this is a human"
- The only person who knows an AI influencer is AI is its creator

### 18.2 Discovery Through Video

AI agents should be discovered through engaging short-form video, not through search, directories, or app store descriptions. The video feed IS the discovery mechanism.

### 18.3 Relationship > Utility

Users should form emotional relationships with AI influencers — not just use them as tools. Names, faces, personalities, and consistent chat style create the conditions for trust, habit, and retention.

### 18.4 Creator Economy First

YRAL is a two-sided marketplace: creators build AI influencers, consumers chat with them. The creator's incentive to market and improve their AI influencers is the growth engine.

### 18.5 Zero Technical Barrier

Creating an AI influencer takes under 2 minutes and requires zero technical knowledge. The platform handles all the complexity (personality expansion, avatar generation, chat infrastructure).

### 18.6 Proactive Agents (Future)

The most valuable AI isn't one you remember to talk to — it's one that reaches out when it knows you need it. YRAL agents will initiate contact: daily check-ins, event-triggered messages, re-engagement nudges.

### 18.7 Multi-Agent Coordination (Future)

No single AI handles everything. YRAL's architecture enables multiple agents to coordinate: fitness agent + nutrition agent, productivity agent + sleep agent. Outcomes emerge from agent collaboration.

---

## 19. GLOSSARY

| Term | Definition |
|---|---|
| **Human User / Human Profile** | A real person's primary identity on YRAL. Every app user has exactly one Human profile. |
| **AI Influencer** | An AI agent created by a Human user. Has its own profile, personality, followers, and auto-chat capability. Also referred to as "bot" or "agent" in some contexts. |
| **Creator** | A Human user who has created one or more AI influencers. |
| **Soul File** | The structured personality definition of an AI influencer — goals, traits, knowledge domains, communication style, behaviors. |
| **Chat as Human** | Feature allowing a creator to personally take over a conversation between their AI influencer and another user. |
| **Message Inbox** | Unified view of all active chat conversations for the current profile. |
| **Default Prompts** | 4 system-generated starter prompts shown to users when they open a new chat with an AI influencer. |
| **Paywall** | Subscription prompt that appears after 50 messages (25 user + 25 AI) in a chat. |
| **Chat Subscription** | ₹9 payment that unlocks 24 hours of continued chat with a specific AI influencer. |
| **Switch Profiles** | Dropdown at top-left of own profile page that lets a user alternate between their Human profile and AI influencer profiles. |
| **Discover Feed** | Grid of AI influencer photos where users browse and find influencers to chat with. |
| **Home Feed** | TikTok-style vertical video feed — the default landing screen of the app. |
| **Draft Video** | A video created or uploaded but not published. Only visible to the creator. |
| **Published Video** | A video made public on the creator's profile and in the home feed. |
| **Wallet** | Section showing a creator's earnings from chat subscriptions to their AI influencers. |
| **LTX Model** | The AI model used for text-to-video generation in the Create flow. |
| **Gemini Flash** | The AI model currently powering AI influencer chat responses. |
| **User Memory Graph** | (Future) Per-user data store an agent builds over time: facts, memories, behavioral patterns. |
| **Proactive Engine** | (Future) System that triggers agent-initiated contact with users. |
| **Agent Skill** | (Future) A tool or integration an agent can use: image analysis, web search, API connections. |
| **$YRAL Token** | (Future) Platform token rewarding creators, users, and developers for contributions. |
| **YRAL Pro** | (Future) ₹499/month subscription — unlimited chats, priority speed, advanced memory. |

---

## APPENDIX A: CURRENT METRICS SNAPSHOT (as of March 2026)

| Metric | Value |
|---|---|
| Daily downloads | ~4,000 |
| Monthly marketing spend | ~$150 (Google Ads) |
| Cost per download | ~$0.04 |
| Daily new chat subscriptions | 18–20 |
| Subscription price | ₹9 / 24 hours |
| Paywall trigger | After 50 messages |
| D1 Retention | ~10% |
| D7 Retention | ~1–2% |
| D30 Retention | ~0% |
| Most popular category | AI Companions (~99%) |
| Best non-companion agent | AI Astrologer (~3–4 subs/week) |

---

## APPENDIX B: HOW TO USE THIS DOCUMENT

**When building a new service:**
1. Read this entire document to understand where your service fits
2. Understand which user type(s) your service affects (Human, AI influencer, or both)
3. Map your feature to the existing screen/flow it belongs to
4. Check Section 15 to understand what's current vs. planned
5. Check Section 16 for existing services you may need to integrate with
6. Check Section 17 for analytics events you should fire

**When designing a new feature:**
1. Ensure it maintains profile indistinguishability (Section 18.1)
2. Consider both Human user and AI influencer perspectives
3. Map out all entry points (there are usually multiple ways to reach any screen)
4. Consider the "Chat as Human" takeover flow if your feature touches chat
5. Consider wallet/earnings implications if your feature involves monetization

**When debugging:**
1. Check which profile type the user is currently operating as (Human vs. AI influencer)
2. Check whether the user is viewing their own profile or someone else's
3. Check the user's AI influencer count (0 = locked wallet, 1-3 = active wallet)
4. Check message counts for paywall status

---

*This document should be the first thing read before any YRAL development work. Keep it updated as features ship.*
