# Veltis Backend

Backend API for Veltis - Biotech IP Tokenization Platform

## Overview

This repository contains the backend API code for the Veltis platform, which enables users to create, fractionalize, list, and trade IP NFTs (Intellectual Property Non-Fungible Tokens) in a decentralized marketplace.

## Tech Stack

- Node.js with Express
- PostgreSQL with Prisma ORM
- JWT authentication with Clerk integration
- Ethers.js for blockchain interaction
- IPFS via NFT.storage

## Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- PostgreSQL database
- Clerk account for authentication

## Development Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/Veltiscapital/veltis-backend.git
   cd veltis-backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file with the following environment variables:
   ```
   # Database
   DATABASE_URL="postgresql://username:password@localhost:5432/veltis"

   # Authentication
   CLERK_SECRET_KEY=your_clerk_secret_key
   JWT_SECRET=your_jwt_secret

   # Blockchain
   POLYGON_AMOY_RPC_URL=your_polygon_amoy_rpc_url
   PRIVATE_KEY=your_private_key_for_contract_interaction

   # Storage
   NFT_STORAGE_API_KEY=your_nft_storage_api_key

   # Server
   PORT=3001
   NODE_ENV=development
   ```

4. Set up the database:
   ```bash
   npx prisma migrate dev
   ```

5. Start the development server:
   ```bash
   npm run dev
   ```

## API Endpoints

### Authentication
- `POST /api/auth/nonce` - Get a nonce for wallet authentication
- `POST /api/auth/verify` - Verify wallet signature
- `GET /api/auth/user` - Get current user information
- `POST /api/auth/logout` - Logout user

### NFTs
- `GET /api/ipnft` - Get all IP NFTs
- `GET /api/ipnft/:id` - Get IP NFT by ID
- `POST /api/ipnft/mint` - Mint a new IP NFT
- `GET /api/ipnft/:id/valuation` - Get valuation for an IP NFT

### Fractionalization
- `GET /api/fractionalization/:address` - Get fractionalization details
- `POST /api/fractionalization` - Create a new fractionalization

### Marketplace
- `GET /api/market/listings` - Get all marketplace listings
- `POST /api/market/listings` - Create a new listing
- `POST /api/market/offers` - Make an offer
- `POST /api/market/accept` - Accept an offer

## Deployment

The backend is deployed to Heroku. Follow these steps to deploy:

1. Create a Heroku app:
   ```bash
   heroku create veltis-backend
   ```

2. Add PostgreSQL addon:
   ```bash
   heroku addons:create heroku-postgresql:hobby-dev
   ```

3. Set environment variables:
   ```bash
   heroku config:set CLERK_SECRET_KEY=your_clerk_secret_key
   heroku config:set JWT_SECRET=your_jwt_secret
   heroku config:set POLYGON_AMOY_RPC_URL=your_polygon_amoy_rpc_url
   heroku config:set PRIVATE_KEY=your_private_key_for_contract_interaction
   heroku config:set NFT_STORAGE_API_KEY=your_nft_storage_api_key
   heroku config:set NODE_ENV=production
   ```

4. Deploy the app:
   ```bash
   git push heroku main
   ```

5. Run database migrations:
   ```bash
   heroku run npx prisma migrate deploy
   ```

## Project Structure

```
├── prisma/              # Database schema and migrations
├── src/
│   ├── controllers/     # Request handlers
│   ├── middleware/      # Express middleware
│   ├── models/          # Data models
│   ├── routes/          # API routes
│   ├── services/        # Business logic
│   ├── utils/           # Utility functions
│   └── index.js         # Entry point
├── .env.example         # Example environment variables
├── package.json         # Project dependencies
└── tsconfig.json        # TypeScript configuration
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.