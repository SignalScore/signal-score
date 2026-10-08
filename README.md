# Signal-Score

A decentralized crypto idea-sharing platform built with Next.js and Soroban smart contracts.


## Project Overview

Signal-Score is a decentralized platform designed for sharing, discovering, and validating cryptocurrency insights and market analysis. It provides an interface for users to browse trending crypto ideas and vote on them. 

The project leverages a modern web stack utilizing Next.js (App Router), React, and Tailwind CSS for the frontend, with multi-language support provided by `next-intl`. On the blockchain side, it integrates with the Stellar network using Soroban smart contracts written in Rust to handle decentralized storage and voting for the ideas. Currently, the backend user sessions and profiles are managed through an in-memory mock store using Next.js Server Actions.

## Table of Contents
- [Key Features](#key-features)
- [Built With](#built-with)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [Running the Project](#running-the-project)
- [API Endpoints](#api-endpoints)
- [Smart Contracts](#smart-contracts)
- [Authentication](#authentication)
- [CI/CD](#cicd)
- [License](#license)

## Key Features

- **Crypto Idea Sharing:** Browse a collection of crypto analysis and market ideas.
- **Smart Contract Integration:** Ideas and their vote counts are stored on-chain via a Soroban smart contract.
- **Vote & Reputation:** Upvote or downvote ideas directly on the blockchain.
- **Multi-language Support:** Full internationalization support for English, Spanish, Chinese, and Arabic.
- **Search and Filtering:** Search API to filter ideas by query, category, tags, and vote counts.
- **Mock Authentication:** Sign up, sign in, and profile settings handled via in-memory server actions.

## Built With

### Frontend
- **Next.js 14:** React framework utilizing the App Router.
- **React 18:** UI library.
- **Tailwind CSS:** Utility-first CSS framework for styling.
- **Radix UI:** Unstyled accessible UI primitives.
- **next-intl:** Internationalization plugin.

### Smart Contracts
- **Rust:** Programming language for the smart contracts.
- **Soroban SDK (v22.0.0):** Stellar's smart contract platform.

### Development & Testing Tools
- **Vitest & Playwright:** Configured dependencies for unit and end-to-end testing.
- **Storybook:** UI component explorer.

## Project Structure

```text
signal-score/
├── app/               # Next.js App Router (pages, layouts, and APIs)
│   ├── [locale]/      # Internationalized routes and server actions
│   └── api/           # API routes for searching and streaming ideas
├── components/        # Reusable React components
├── hooks/             # Custom React hooks for contract integration
├── lib/               # Utility functions and in-memory data store
├── messages/          # Localization JSON files (ar, en, es, zh)
├── src/               # Rust source code for Soroban smart contracts
├── Cargo.toml         # Rust package manifest
└── package.json       # Node.js dependencies and scripts
```

## Installation & Setup

### Prerequisites
- **Node.js:** v18 or newer
- **Rust:** Latest stable toolchain (for smart contract development)

### Frontend Installation

1. Clone the repository and navigate into it:
   ```bash
   git clone https://github.com/SignalScore/signal-score.git
   cd signal-score
   ```

2. Install the Node.js dependencies:
   ```bash
   npm install
   ```

## Running the Project

### Development Server
To start the Next.js frontend in development mode:

```bash
npm run dev
```
The application will be available at `http://localhost:3000`.

### Production Build
To build and start the production-optimized application:

```bash
npm run build
npm run start
```

### Storybook
To run the Storybook component explorer:

```bash
npm run storybook
```

## API Endpoints

The project includes custom backend API routes within the Next.js `app/api/` directory.

### `GET /api/ideas/search`
Searches and filters through the ideas database.
- **Query Parameters:**
  - `q` (string): Search text.
  - `category` (string): Filter by category.
  - `tags` (string): Comma-separated list of tags.
  - `contentType` (string): `premium`, `free`, or `all`.
  - `authors` (string): Comma-separated list of authors.
  - `voteMin` / `voteMax` (number): Filter by vote ranges.
  - `limit` (number): Pagination limit (max 50).
  - `cursor` (number): Pagination offset.
- **Response:** Returns a JSON object containing `results`, `total`, and a `nextCursor`.

## Smart Contracts

The project utilizes a Soroban smart contract located in `src/main.rs`. 

**Key Functions:**
- `create_idea(title, content, author, is_premium, tags)`: Registers a new idea on the ledger and initializes its vote count.
- `vote_idea(idea_id, is_upvote)`: Increments or decrements the vote count for a given idea.
- `get_idea(idea_id)`: Retrieves a specific idea's data.
- `get_ideas_paginated(sort_by, cursor, limit)`: Returns paginated ideas sorted by newest, most votes, or trending.

**Testing the Contract:**
Run the Rust test suite using Cargo:
```bash
cargo test
```

## Authentication

Authentication is handled via Next.js Server Actions located in `app/[locale]/actions/auth.js`. 
> **Note:** The current implementation uses an in-memory mock data store (`globalThis.__signalScoreAuthStore`) to manage user accounts and sessions. It uses standard cookies for session tracking but does not persist data across server restarts. There is no real production database configured.

## CI/CD

The repository contains a GitHub Actions workflow for Storybook located at `.github/workflows/storybook.yml`.

## License

This project is licensed under the [MIT License](LICENSE).
