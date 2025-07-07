# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Presence.AI** is an AI-powered SaaS platform designed to automate social media lead generation and outreach for freelancers. The platform addresses the problem that 30% of freelancers' time is spent chasing leads manually across platforms like Twitter, Reddit, LinkedIn, and Upwork.

### Core Product Vision
Three-part solution:
1. **Lead Finding** - Scraping opportunities from social platforms using AI filtering
2. **Automated Outreach** - AI-generated comments, DMs, and replies to potential clients
3. **Presence Building** - Automated posting and engagement to build professional visibility

### MVP Strategy
Starting with Twitter-focused lead generation:
- Twitter hashtag/keyword monitoring (#hiring, #freelance)
- Automated personalized DMs to potential clients
- Scheduled portfolio posts and engagement
- Email digest of curated leads

## Development Commands

```bash
# Start development server
npm run dev
# or
pnpm dev

# Build for production
npm run build

# Start production server
npm start

# Run linter
npm run lint
```

## Technical Architecture

### Core Stack
- **Framework**: Next.js 15 with App Router
- **Database**: PostgreSQL with Prisma ORM
- **Authentication**: NextAuth.js with GitHub OAuth
- **Styling**: Tailwind CSS with shadcn/ui components
- **TypeScript**: Full TypeScript setup

### Authentication Flow
1. GitHub OAuth via NextAuth.js (targeting freelancers)
2. Custom login API endpoint (`/api/auth/login`) handles user creation/lookup
3. JWT tokens generated for authenticated sessions
4. Custom session/user types defined in auth options

### Database Schema
Current `User` model with fields:
- `id` (auto-increment primary key)
- `name`, `email` (required)
- `provider`, `oauth_id` (OAuth provider info)
- `image` (optional profile image)
- `created_at` (timestamp)

*Note: Schema will need expansion for freelancer profiles, skills, lead tracking, and platform integrations*

### Planned Integrations
- **Twitter API** - Lead scraping, DM automation, posting
- **Reddit API** - Subreddit monitoring (r/forhire, r/freelance, niche subreddits)
- **LinkedIn API** - Professional networking automation
- **AI/NLP** - GPT-based models for context-aware response generation

### Environment Variables Required
- `DATABASE_URL` - PostgreSQL connection string
- `GITHUB_CLIENT_ID` - GitHub OAuth app ID
- `GITHUB_CLIENT_SECRET` - GitHub OAuth app secret
- `JWT_SECRET` - Secret for JWT token signing
- `NEXTAUTH_SECRET` - NextAuth.js secret
- `NEXT_PUBLIC_APP_URL` - Application URL
- `TWITTER_API_KEY` - Twitter API access (planned)
- `OPENAI_API_KEY` - AI response generation (planned)

### Component Library
Uses shadcn/ui with Tailwind CSS:
- Components configured in `components.json`
- Custom color scheme with CSS variables
- Lucide React for icons
- Radix UI primitives for accessible components

### Compliance Considerations
- **Platform Rate Limits**: Twitter DM limits (1,000/day), Reddit anti-spam delays
- **Authentication**: OAuth flows for secure platform access
- **Content Quality**: AI-generated responses must avoid spam detection
- **User Safety**: Manual review options for AI-generated content

### Key Implementation Details
- Uses pnpm as package manager
- Custom TypeScript interfaces for NextAuth session/user types
- Hardcoded localhost URL in auth configuration (app/api/auth/[...nextauth]/options.ts:38)
- Prisma client configured with query logging in development
- Database operations handled in `/app/api/auth/login/route.ts`

### Pricing Strategy
- Target: $5-10/month for freelancers
- Free tier for basic lead alerts
- Revenue model based on time savings (10+ hours/week) and ROI (landing gigs)