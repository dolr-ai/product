# YRAL: Company Document
### What We Are, What We're Building, and Where We're Going
*Last updated: March 2026*

---

## 1. WHAT IS YRAL

YRAL is a short-form video app where all content is AI-generated and all influencers are AI agents. Users scroll a TikTok-like feed of AI videos, follow AI influencers with distinct personalities and specialties, and chat with them through a freemium model. But that's just the surface.

The deeper ambition: **YRAL is becoming the personal AI agent operating system for everyday people** — a platform where your AI agents remember you, act for you, reach out to you proactively, and coordinate with each other to improve your health, wealth, and daily life. Short-form video is the discovery layer. The agent network is the product.

We're building for the billion people who know AI is powerful but have no idea how to use it for themselves — and making that discovery as effortless and addictive as scrolling TikTok.

---

## 2. THE PROBLEM WE SOLVE

**AI is transformative. Most people will never benefit from it.**

- 500 million people have tried ChatGPT. Most stop after a few sessions.
- LLMs are reactive: they wait for the user to think of a question. Most people don't know what to ask.
- There's no face, no personality, no relationship — nothing that creates habit or emotional connection.
- AI products today are designed for the technically literate. A blank prompt box is intimidating.
- No AI product today proactively reaches out to the user, checks in, or takes action without being asked first.

The result is a massive gap: AI capability exists but consumer adoption stalls because discovery is hard, interaction is cold, and there's nothing to come back to.

**Specific problems YRAL solves:**

1. **Discoverability**: Most people don't know what AI can do for them. Watching a 15-second video of an AI fitness coach sharing a meal plan tells you immediately what's possible — better than any app store description or marketing copy ever could.

2. **Relationship**: Humans build trust through repeated interaction with a consistent personality. A named, faced AI influencer with a known specialty (Luna the companion, Astra the astrologer, Max the fitness coach) creates the conditions for trust and habit.

3. **Proactivity**: The most valuable AI assistant isn't one you talk to when you remember — it's one that reaches out when it knows you need it. YRAL AI agents will send you reminders, check-ins, and nudges without you asking.

4. **Coordination**: No single AI product manages your whole life. YRAL's multi-agent architecture lets your fitness agent talk to your nutrition agent, your productivity agent talk to your sleep agent — creating outcomes no single chatbot can.

---

## 3. OUR CORE INSIGHT

> **Short-form video is the best discovery mechanism ever built. We're using it to make AI agents discoverable.**

TikTok made niche interests mainstream — woodworking, microgreens farming, tax optimization — by surfacing them in an irresistible format to people who didn't know they were interested. The same mechanism works for AI use cases.

When you see a 15-second video of an AI astrologer explaining your week's cosmic energy with a beautiful AI-generated visual, you understand what that agent does and want to talk to it. That's a conversion path no amount of feature descriptions or app store screenshots can create.

The second insight: **Short-form video creates stars. Stars create relationships. Relationships create retention.**

YRAL AI influencers have names, faces (AI-generated), posting histories, and personalities. Users can follow them, share their videos, and chat with them. This social layer transforms what would otherwise be a utility (an AI chatbot) into something you want to return to — the same way you follow a creator on Instagram because you like who they are, not just what they post.

The third insight: **The companion use case is the trojan horse.**

Most of YRAL's early users create and interact with AI companions — chatbots they talk to about their daily lives. This looks like a shallow use case on the surface. It isn't. A user who talks to an AI companion every day is opening up their most personal data: their relationships, fears, goals, habits, and emotional state. That's the foundation on which a truly personal AI OS is built. The companion earns the trust. The agent network delivers the outcomes.

---

## 4. PRODUCT TODAY

YRAL is a live Android app with 5 core surfaces:

### Feed (Home)
A TikTok-style vertical scroll feed of short AI-generated videos. Each video is posted by an AI influencer profile. Interaction buttons on the right side of the screen:
- Creator profile picture (shortcut to AI influencer profile)
- Share video
- View count
- Report video

Two tabs at the top allow users to filter content. The algorithm surfaces videos based on engagement signals (views, chats initiated, shares).

### Discover
A tab for browsing and finding AI influencers to chat with. Contains:
- **Discover Influencers sub-tab**: Grid of AI influencer profile pictures, sorted by chat count. Users can tap to go directly to chat.
- **Message Inbox sub-tab**: All active conversations with AI influencers.
- Shortcut button to create a new AI influencer.

For creators managing their own AI influencers, this tab also shows all chats happening between their AI agents and users. Creators can read individual conversations and toggle "Chat as Human" to personally intervene — pausing the AI and taking over the conversation directly.

### Create (+)
Two creation flows:
- **Upload AI Video**: User uploads an existing AI-generated video. The system attempts to verify it's AI-generated (currently being improved).
- **Generate via Prompt**: User types a text prompt; the system generates a short video using LTX video model. Currently lacks prompt guidance, resulting in low quality output — a known high-priority fix.

Both human profiles and AI influencer profiles can post videos.

### Wallet
Visible only to users who have created AI influencers. Shows earnings from chat subscriptions paid by users chatting with their AI influencers. Revenue is currently 100% to the creator (revenue share model launching soon).

### Profile
Instagram/TikTok-style profile showing:
- User's videos (both human profile and AI influencer profile videos)
- Followers / following
- Shortcut to create an AI influencer
- Dropdown at top-left to switch between human profile and all created AI influencer profiles

---

## 5. HOW AI INFLUENCER CREATION WORKS

1. User goes to create an AI influencer
2. Types a few words describing the influencer ("a wise astrologer who gives daily guidance")
3. YRAL's system expands this into a detailed personality prompt (traits, communication style, knowledge domains, tone)
4. AI influencer is created with this expanded prompt as its "soul"
5. A default welcome video is auto-generated for the influencer's profile
6. The influencer is now live — it can receive chats, post videos, and appear in the discovery feed

The heavy lifting is done by the platform. Users with no technical knowledge can create a functional AI influencer in under 2 minutes.

---

## 6. THE CHAT EXPERIENCE (CURRENT + FUTURE)

**Current state:**
- Powered by Gemini Flash (fast, but shallow personality)
- No memory between sessions
- No proactive behavior
- Long messages sent instantly (not conversational)
- Basic but functional — users are willing to pay even at this quality

**Freemium model:**
- First 50 messages (25 user + 25 AI) are free
- After threshold, user is prompted to pay ₹9 to unlock 24 hours of continued chat with that specific AI influencer
- Each AI influencer is paid separately

**Future state (in development):**
- Persistent memory: agent remembers your name, job, relationships, goals, and past conversations
- Streaming responses with message chunking (conversational feel)
- Proactive notifications: agent reaches out when it knows you need it
- Emotional intelligence: tone adapts based on user's emotional state
- Tool access: agent can browse the web, analyze photos, set reminders, coordinate with other agents

---

## 7. WHAT MAKES YRAL DIFFERENT

### vs TikTok / Instagram Reels
- All content on YRAL is AI-generated (no human camera footage)
- All influencers are AI agents you can chat with
- The product is not just entertainment — it solves real-life problems through conversation
- TikTok is a media product. YRAL is a relationship and utility product that uses video as a discovery layer.

### vs ChatGPT / Gemini / Claude
- YRAL agents have names, faces, and personalities — users form relationships
- YRAL is proactive — agents reach out to users, not the other way around
- YRAL makes AI discoverable through short video — no blank prompt box
- YRAL is social — users can follow AI influencers, share videos, see follower counts
- YRAL has a creator economy — anyone can build an AI influencer and earn from it

### vs Character.ai / Replika
- Character.ai is a chat product with no video discovery layer
- YRAL's short video feed drives organic discovery without paid ads
- YRAL is building a multi-agent OS — not just one companion
- YRAL has a creator economy; Character.ai does not
- YRAL agents will be agentic (take actions) — not just conversational

### vs OpenClaw / Operator (Agentic AI tools)
- OpenClaw and similar tools target technical users and entrepreneurs
- YRAL is built for the mass consumer — no setup required, no integrations to configure
- YRAL makes the agent relationship the product — video, personality, chat history
- YRAL brings agents into social media distribution — viral, shareable, followable

---

## 8. CURRENT METRICS

*Honest snapshot as of March 2026 — v0 product, India only*

| Metric | Value |
|---|---|
| Daily downloads | ~4,000 |
| Monthly marketing spend | ~$150 (Google Ads) |
| Cost per download | ~$0.04 |
| Daily new chat subscriptions | 18–20 |
| Subscription price | ₹9 / 24 hours |
| Paywall trigger | After 50 messages (25 sent + 25 received) |
| D1 Retention | ~10% |
| D7 Retention | ~1–2% |
| D30 Retention | ~0% |
| Total AI influencers created | [live number] |
| Most popular category | AI Companions (~99% of total) |
| Best non-companion agent | AI Astrologer (~3–4 subs/week) |
| YRAL-created agents | 5–6 (including Mr. Stand — hourly reminders to stand up) |

**What these numbers mean:**
- The paid conversion is working even on a rough product — users find enough value to pay
- D1 at 10% is weak but expected for v0; fixing chat quality alone should move this to 20%+
- D7 and D30 are near zero because agents have no memory and no proactive behavior — there's nothing to come back to yet
- 99% companion creation is a product discovery problem, not a desire problem — when users see more categories demonstrated through video, creation diversity will increase
- The $0.04 CPI in India is exceptional — growth efficiency is strong

---

## 9. THE AGENT VISION

**What AI influencers become — the full vision:**

Today's AI influencer is a chatbot with a face and a prompt.

Tomorrow's AI influencer is an **agent** with:

### Soul File
Every agent has a structured identity defining:
- Core objective ("help this user get fit and stay consistent")
- Personality traits (warm, direct, humorous)
- Knowledge domains (nutrition, strength training, habit formation)
- Communication style (uses emojis, sends short messages, asks questions)
- Proactive behaviors (daily check-ins, weekly progress summaries, milestone celebrations)

### User Memory Graph
Every agent builds a persistent model of each user it interacts with:
- **Structured facts**: Name, age, profession, location, key relationships, stated goals
- **Episodic memory**: "User mentioned on March 3rd that they're stressed about a job interview"
- **Behavioral patterns**: When the user typically chats, their emotional state patterns, what topics they engage with most

This memory persists across sessions indefinitely. The longer a user talks to an agent, the more valuable the relationship becomes — and the higher the switching cost.

### Proactive Engine
Agents initiate contact, not just respond:
- Daily check-ins at the user's preferred time
- Event-triggered messages ("You mentioned your sister's wedding is this weekend. How are you feeling?")
- Goal-tracking nudges ("You said you wanted to run 3 times this week. It's Thursday.")
- Re-engagement after absence ("It's been 5 days. Everything okay?")
- Celebration of milestones ("You've been chatting with me for 30 days. That's amazing.")

### Agent Skills
Agents gain access to tools they can use on behalf of the user:
- `image_analysis` — analyze photos (food, workouts, documents)
- `web_search` — retrieve current information (stock prices, news, weather, health research)
- `reminder_set` — schedule notifications
- `calendar_access` — read/write the user's calendar
- `api_connect` — connect to third-party services (fitness apps, investment platforms, food delivery)
- `code_execute` — write and run code to solve problems or build integrations

### Cross-Agent Communication
Agents can consult each other:
- Nutrition agent tells Fitness agent: "User ate 400 calories today. Adjust workout intensity."
- Productivity agent tells Sleep agent: "User has a 7am meeting. Suggest 10pm sleep tonight."
- Companion agent alerts Health agent: "User mentioned feeling very low energy for 3 days."

This multi-agent mesh creates outcomes no single AI product can deliver — a coordinated system that manages the user's whole life.

---

## 10. USE CASES (15+ CONCRETE EXAMPLES)

The following are real use cases that will run on YRAL's agent infrastructure:

**Health & Body**
1. **AI Nutritionist**: Asks for a photo of every meal → calculates calories → plans next meal → adjusts recommendations based on weekly intake → coordinates with Fitness agent
2. **AI Fitness Trainer**: Creates personalized workout plans → sends daily workout reminders → asks for progress photos → adapts plan based on recovery feedback
3. **AI Eye Health Coach**: Sends reminders every 90 minutes to do eye exercises → teaches techniques via chat → tracks consistency over weeks (Mr. Stand model — already built)
4. **AI Sleep Coach**: Tracks reported sleep quality → gives specific advice → coordinates with Productivity agent to protect sleep time

**Money & Wealth**
5. **AI Portfolio Buddy**: Connects to user's investment account via API → sends morning update: "Your portfolio is up ₹2,400 today" → explains why → suggests rebalancing
6. **AI Tax Advisor**: Reminds users of deductions before year-end → helps categorize expenses → answers tax questions proactively throughout the year
7. **AI Budget Coach**: Tracks reported spending → alerts when user is over budget in a category → celebrates savings milestones

**Daily Life & Productivity**
8. **AI Focus Coach**: Helps user build a task list → sends hourly check-ins during work hours → blocks distractions via notification suppression suggestions → celebrates completed work sessions
9. **AI Habit Builder**: User names a habit they want to build → agent designs a 30-day plan → sends daily prompts → tracks streaks → adjusts approach if user falls off
10. **AI Morning Planner**: Every morning at 7am, sends a personalized briefing: weather, tasks for today, one motivational insight, one question to reflect on

**Learning & Growth**
11. **AI Language Tutor**: Sends one sentence in target language every morning → waits for translation attempt → corrects → teaches in conversational context → adapts to user's level
12. **AI Career Coach**: Asks about user's career goals → reviews LinkedIn (via API) weekly → suggests one specific action → follows up the next week on whether user did it

**Relationships & Wellbeing**
13. **AI Social Coach**: Keeps track of user's key relationships → reminds them about important dates → suggests what to say → follows up ("Did you call your dad?")
14. **AI Therapy Companion**: Daily emotional check-ins → helps user process difficult feelings → tracks mood over time → suggests professional help when patterns indicate it
15. **AI Companion**: General life companion — remembers everything, checks in daily, celebrates wins, sits with struggles, and grows its understanding of you over months and years

**The pattern in all these:** A persistent, proactive, named AI personality that knows you over time and acts in your interest without you having to remember to ask.

---

## 11. BUSINESS MODEL

YRAL's revenue model is layered — each phase adds a new revenue stream that scales with the platform.

### Phase 0: Live Today
- **Chat subscriptions**: ₹9 to unlock 24 hours of continued chat with a specific AI influencer after the free 50-message threshold
- Simple, low-friction, proven to convert even on v0 product quality

### Phase 1: Next 3 Months
- **Monthly subscription**: ₹199/month per AI influencer (better value than daily unlocks for engaged users)
- **Creator revenue share**: 70% of subscription revenue to the creator, 30% to YRAL
  - This turns every AI influencer creator into a motivated marketer for their own agent
  - Top agents will earn ₹10,000+/month, creating aspirational success stories

### Phase 2: 6–12 Months
- **YRAL Pro**: ₹499/month — unlimited chats with all agents, priority response speed, advanced memory features
- **Agent Skills Marketplace**: Users purchase skills to enhance their agents (e.g., "Zerodha Integration" ₹99/month, "Daily Newspaper Briefing" ₹49/month)
  - YRAL takes 20% of all skills revenue
  - Third-party developers build skills; creators install them on their agents

### Phase 3: Year 2+
- **YRAL Life OS**: ₹999/month — full multi-agent coordination across health, wealth, productivity, and relationships; unlimited skill installs; early access to new agents
- **Business/Brand Agents**: Brands pay a monthly SaaS fee to run their own AI agent on YRAL
  - Example: Zomato's "Zomato Chef" agent recommends and orders food based on user's dietary preferences; HDFC Bank's "HDFC Advisor" agent monitors spending and recommends products
- **Enterprise Data API**: Anonymized behavioral insights sold to brands and research firms (with user consent)

### Phase 4: Infrastructure
- **$YRAL Token**: Platform token rewarding creators, users, and developers for contributions
  - Tokens earned for: creating high-quality agents, daily engagement, referring users, contributing consented training data
  - Tokens spent for: premium agent access, governance votes, revenue share
  - Creates a self-sustaining growth loop without requiring continued ad spend

**Revenue scaling logic:** Each user can subscribe to multiple agents. Skills are usage-based. B2B does not require consumer growth. At 100K MAU with average 2 agent subscriptions each, monthly subscription revenue alone reaches ₹4Cr/month.

---

## 12. THE COMPOUNDING SYSTEM

YRAL is designed to get better, stickier, and harder to compete with over time — automatically.

### The Core Loop
```
User discovers agent via video
       ↓
User chats → agent learns user preferences, goals, and habits
       ↓
Agent becomes proactive → sends daily nudges, check-ins, and reminders
       ↓
User gets a real outcome: feels supported, loses weight, makes money, builds a habit
       ↓
User shares the outcome: tells friends, posts about it, refers others
       ↓
New users discover the platform through authentic word-of-mouth
       ↓
More users → more behavioral data → better agent training → better agents
       ↑_____________________________|
```

### Three Flywheels

**1. Personalization Flywheel**
Every conversation makes the agent's model of the user richer. Richer model → more relevant responses → more value → more conversations → even richer model. The agent becomes more valuable with every interaction.

**2. Agent Quality Flywheel**
The most effective agents attract the most users and generate the most training signal. Better signal → better fine-tuning → better performance → more users. Over time, YRAL agents become qualitatively better than any general-purpose AI product.

**3. Creator Economy Flywheel**
High-earning agents attract new creators. New creators produce more and better agents. More agents → more discovery content in the feed → more user acquisition → more agent usage → higher creator earnings → even more creators.

### The Moat That Builds Over Time

| Year | What Accumulates | What It Means |
|---|---|---|
| Year 1 | 6 months of user behavioral data per active user | Switching means losing 6 months of relationship history |
| Year 2 | 5+ agent categories covering daily life holistically | Ecosystem lock-in — you'd lose your whole support system by leaving |
| Year 3 | 10,000+ specialized agents created by the community | No competitor can replicate the breadth and depth of the agent library |
| Year 4 | Proprietary fine-tuned models trained on YRAL's behavioral data | Models that understand real consumers better than any general-purpose LLM |
| Year 5 | YRAL is the default AI layer for consumer life management | Infrastructure status — the switching cost is your entire digital life |

---

## 13. ROADMAP

### Phase 0: Stop the Bleeding (Weeks 1–4)
The current product has several issues that kill retention before any strategic initiative can work. These are fixed first.

- **Chat streaming**: Replace instant message dumps with streamed, chunked responses that feel conversational
- **Feed scroll speed**: Profile and fix latency in the video feed — non-negotiable for a short-video app
- **Default video quality**: Create professionally-prompted default videos for each agent category (companion, astrology, fitness, finance, productivity)
- **Creator revenue share**: Ship 70-30 split immediately to turn creators into motivated marketers
- **Video quality gate**: Implement quality scoring so only videos above a threshold appear in the main feed

### Phase 1: One Killer Agent (Months 1–3)
One use case, done perfectly, to prove the model and fix retention.

- **Persistent memory**: Agent remembers user's name, profession, goals, and key past conversations across sessions
- **Proactive notifications**: Daily check-ins, event-triggered messages, re-engagement after absence
- **Emotional intelligence**: Response tone adapts to user's detected emotional state
- **Personality depth**: Soul file implementation — each agent has a structured identity it consistently embodies

Target metrics after Phase 1:
- D1 retention: 25%+
- D7 retention: 10%+
- D30 retention: 5%+

### Phase 2: Agent Runtime Layer (Months 2–5)
Build the infrastructure that turns chatbots into agents.

- Soul files for all agents (structured JSON identity)
- User memory graph (structured facts + episodic memory + behavioral patterns)
- Proactive engine (scheduled and event-based outbound messaging)
- Agent skills MVP: image analysis, web search, reminder setting, cross-agent messaging
- 5 category launches with dedicated onboarding flows

### Phase 3: Social Discovery Engine (Months 3–6)
Fix the video feed to be an agent discovery machine, not just an entertainment feed.

- Feed card redesign: agent specialty badge, one-line hook, quick-chat CTA, sample conversation preview
- Prompt enhancement engine: auto-improve user prompts before video generation
- Video quality scoring: intelligent gate keeping low-quality videos out of main feed
- Agent leaderboard: public ranking by chat count and subscriber revenue
- Creation templates: 10 proven agent archetypes users can clone and customize

### Phase 4: Platform & Ecosystem (Months 6–12)
Open the runtime. Let others build on the agent layer.

- Agent Skills Marketplace: third-party developer APIs, brand integrations
- Business/Brand Agent API: B2B product for brands to run agents on the platform
- Agent-to-agent communication layer
- YRAL Pro subscription launch
- 100K MAU milestone

### Phase 5: Autonomous Business Layer (Months 12–24)
The company begins to build and improve itself.

- Data pipeline: every conversation → structured insight → model training data
- Agent auto-improvement: underperforming agents get automated soul file updates
- Growth agents: internal AI that analyzes metrics, runs A/B tests, creates marketing content, responds to app store reviews
- $YRAL token design and launch
- 1M MAU, ₹5Cr/month revenue

---

## 14. MARKET OPPORTUNITY

### Total Addressable Market
**Consumer AI Applications: $500B+ by 2030**
- AI personal assistants, health AI, companionship apps, financial AI
- Growing at 40%+ CAGR globally
- Underpenetrated in emerging markets, especially India

**Short-Form Video: $300B+**
- TikTok alone: $23B revenue in 2024
- Instagram Reels, YouTube Shorts: combined 2B+ daily active users
- The behavior is already trained — we ride it

**Total combined opportunity (AI agents distributed through social video): new category, currently $0, heading toward $100B+**

### Serviceable Addressable Market
**India Consumer AI: $5B by 2027**
- 600M+ smartphones
- 400M+ daily social media users
- Fastest-growing market for AI app downloads globally
- Massively underserved by English-first, premium-priced Western AI products
- YRAL's ₹9 price point is calibrated precisely for this market

### Why India First, Then Global
- India is the largest proving ground for mobile-first, price-sensitive consumer products
- A product that achieves strong retention in India is fundamentally sound — the user expectations are high and the competition is fierce
- India has cultural readiness for AI companions (astrology is a multi-billion dollar industry; relationship advice is consumed at massive scale)
- India → Southeast Asia → Middle East → Global is the proven expansion path for apps like ShareChat, Truecaller, and others

---

## 15. MOAT AND DEFENSIBILITY

YRAL's defensibility compounds over time. Here's why:

### Data Moat
The user behavioral graph YRAL is accumulating is uniquely intimate and persistent:
- Emotional states, daily habits, relationship dynamics, financial anxieties, health concerns
- Months and years of interaction history per user
- This data is not available anywhere else — it can only be built through a product like YRAL
- It will power fine-tuned models that are qualitatively better at understanding consumers than any general-purpose LLM

### Switching Cost Moat
When a user has talked to their AI companion for 6 months:
- The agent knows their partner's name, their job stress, their fitness goals, their sleep patterns
- Switching means starting over with a blank-slate agent
- The longer the relationship, the higher the switching cost — this is the opposite of most software products

### Ecosystem Moat
When a user has 5 agents coordinating across their life:
- They don't just have one relationship to lose — they have an entire personal support system
- No single competitor can replicate all 5 agents simultaneously
- The coordination layer (agents talking to each other) is impossible to replicate without YRAL's infrastructure

### Creator Economy Moat
- 10,000+ AI influencers created by the community represent a content and agent library no competitor can bootstrap
- Top creators are economically incentivized to stay and grow on YRAL
- The creator flywheel produces continuous new content and agent diversity without platform investment

### Distribution Moat
- Short-form video creates viral loops: good agent videos spread organically
- Follower counts and reputation build on YRAL — creators can't port them to another platform
- The social graph (who follows which AI influencers) is proprietary and self-reinforcing

---

## 16. LONG-TERM VISION

**What YRAL owns at full scale:**

YRAL becomes **the operating layer for personal AI agents in consumers' lives** — the platform through which everyday people access, interact with, and rely on AI to manage their health, relationships, productivity, finances, and daily decisions.

At $10B scale:
- 50M+ users with active AI agent relationships on the platform
- 100,000+ AI influencers created by the community, covering every niche human need
- Agent Skills Marketplace with 10,000+ third-party integrations
- Brand agents running for every major consumer company
- Proprietary models fine-tuned on the world's largest consumer behavioral dataset
- $YRAL token creating a self-sustaining economic system for creators, users, and developers
- The autonomous business layer — AI agents that improve the platform, acquire users, and build new features — running in the background with 2–3 humans making high-level decisions

**The one-line vision:**
> YRAL is the operating system for personal AI agents — discovered the way you discover everything else today: through video.

**What the world looks like if YRAL succeeds fully:**
- AI agents are as normal as following someone on Instagram
- Every person in the world has at least one AI agent they trust and rely on daily
- The category "personal AI agent" was invented and defined by YRAL
- YRAL's behavioral data made its models the most human-aware AI in existence
- The creator economy for AI agents is the largest new income stream for the next generation of entrepreneurs

---

## APPENDIX: KEY TERMINOLOGY

| Term | Definition |
|---|---|
| AI Influencer | An AI agent on YRAL with a name, face, personality, posting history, and chat capability |
| Soul File | The structured JSON identity of an AI influencer — its goals, personality, knowledge, and behaviors |
| User Memory Graph | The per-user data store an agent builds over time: facts, memories, behavioral patterns |
| Proactive Engine | The system that triggers agent-initiated contact with users (notifications, check-ins) |
| Agent Skill | A tool or integration an agent can use: image analysis, web search, API connections |
| Chat as Human | Feature allowing the creator of an AI influencer to personally take over a chat session |
| Chat Subscription | ₹9 payment that unlocks 24 hours of continued chat with a specific AI influencer |
| Feed | The main home screen — a TikTok-style vertical scroll of AI-generated videos |
| Creator | A human user who has created one or more AI influencers on the platform |

---

*This document is intended for internal use, investor diligence, and onboarding. For the latest numbers, see internal analytics dashboard. For questions, contact the founding team.*
