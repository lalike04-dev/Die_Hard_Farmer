D-H Farmer Backend
A robust RESTful API powering the D-H Farmer agricultural platform.

📖 Overview
D-H Farmer is a backend service designed to connect farmers and buyers through a feature-rich API. It enables farmers to receive AI-driven advice, compete on a leaderboard, and establish formal contracts with buyers. Buyers can discover top-rated farmers, post applications, and manage contracts—all validated and secured with modern TypeScript tooling.

✨ Features
1. AI Assistant for Farmers
Answers questions about fertilizer selection, efficiency maximization, crop selection, planting schedules, etc.

Integrates with LLM providers (e.g., OpenAI, Gemini) via a dedicated service.

Context-aware responses based on farmer's location, soil data, and historical yields.

2. Farmer Leaderboard
Ranks farmers based on:

Crop yield (tons per hectare)

Sales volume and revenue

Customer ratings (1-5 stars)

Overall efficiency score (computed algorithmically)

Supports filtering by region, crop type, and time period.

Publicly accessible and updated in real-time.

3. Farmer Discovery for Customers
Browse farmers sorted by rating, price, and availability.

View detailed profiles: price listings, available crops, farm land location (map coordinates).

Search and filter by crop, location, rating, and price range.

4. Buyer Applications & Competitive Bidding
Buyers post applications specifying crop type, quantity, quality standards, and maximum price.

Farmers (or groups) submit bids with their offered price and quality guarantees.

System ranks bids by quality-to-price ratio and notifies the buyer.

5. Formal Contract Establishment
Generate digital contracts between buyers and farmers/groups.

Contract details include:

Price per unit

Total quantity

Crop type(s)

Delivery schedule

Recurring or one-time purchase

Penalty clauses and quality assurance terms

Contracts are stored securely and can be exported as PDF.

🛠 Tech Stack
Runtime: Node.js (v18+)

Language: TypeScript

REST Framework: Express.js

Validation: Zod

Database: PostgreSQL (via Prisma) – adjustable

Authentication: JWT (JSON Web Tokens)

AI Integration: OpenAI API / compatible LLM endpoint

Testing: Jest + Supertest

Linting: ESLint + Prettier

Logging: Winston / Pino

Documentation: Swagger / OpenAPI

🚀 Getting Started
Prerequisites
Node.js >= 18.x

npm or yarn

PostgreSQL (or your preferred database)

An API key for the AI service (e.g., OpenAI)

Installation
bash
git clone https://github.com/your-org/d-h-farmer-backend.git
cd d-h-farmer-backend
npm install
Environment Variables
Create a .env file in the root directory:

env
# Server
PORT=3000
NODE_ENV=development

# Database
DATABASE_URL="postgresql://user:password@localhost:5432/dhfarmer"

# JWT
JWT_SECRET=your_super_secret_key
JWT_EXPIRES_IN=7d

# AI Service
AI_API_KEY=sk-...
AI_MODEL=gpt-4o-mini

# External Services (optional)
MAPS_API_KEY=...
Running the Application
bash
# Development (with hot reload)
npm run dev

# Build for production
npm run build

# Start production server
npm start
📜 Available Scripts
npm run dev – Start development server with nodemon/ts-node-dev

npm run build – Compile TypeScript to JavaScript

npm start – Run compiled production build

npm run lint – Run ESLint

npm run format – Run Prettier

npm test – Run Jest tests

npm run test:watch – Run tests in watch mode

npm run prisma:migrate – Run database migrations

npm run prisma:generate – Generate Prisma client

🗂 Project Structure
text
src/
├── config/           # Environment and app configuration
├── controllers/      # Request handlers
├── middlewares/      # Express middlewares (auth, error, validation)
├── models/           # Database models (Prisma schema)
├── routes/           # API route definitions
├── services/         # Business logic (AI, contracts, leaderboard)
├── utils/            # Helper functions (logger, errors, etc.)
├── validators/       # Zod schemas for request validation
├── types/            # TypeScript type definitions
├── app.ts            # Express app setup
└── server.ts         # Entry point
🔌 API Endpoints (Overview)
Authentication
POST /api/auth/register – Register a new user (farmer or buyer)

POST /api/auth/login – Login and receive JWT

GET /api/auth/me – Get current user profile

Farmers
GET /api/farmers – List farmers (with filters: rating, location, crop)

GET /api/farmers/:id – Get farmer details

PUT /api/farmers/:id – Update farmer profile (auth required)

GET /api/farmers/:id/crops – List available crops and prices

Leaderboard
GET /api/leaderboard – Get global leaderboard

GET /api/leaderboard/region/:region – Filter by region

GET /api/leaderboard/crop/:crop – Filter by crop type

AI Assistant
POST /api/ai/ask – Submit a question to the AI assistant

GET /api/ai/history – Get past queries (auth required)

Buyer Applications
POST /api/applications – Create a new application (buyer only)

GET /api/applications – List open applications

GET /api/applications/:id – Get application details

POST /api/applications/:id/bids – Submit a bid (farmer only)

GET /api/applications/:id/bids – List bids for an application

Contracts
POST /api/contracts – Create a contract from an accepted bid

GET /api/contracts – List contracts for the authenticated user

GET /api/contracts/:id – Get contract details

PATCH /api/contracts/:id – Update contract status (e.g., signed, completed)

GET /api/contracts/:id/pdf – Download contract as PDF

✅ Validation with Zod
All incoming requests are validated using Zod schemas. Schemas are defined in src/validators/ and applied via a custom middleware. Example:

typescript
import { z } from 'zod';

export const createApplicationSchema = z.object({
  cropType: z.string().min(1),
  quantity: z.number().positive(),
  maxPrice: z.number().positive(),
  qualityStandard: z.string().optional(),
  deadline: z.string().datetime(),
});
🧪 Testing
Unit tests for services and utilities.

Integration tests for API endpoints using Supertest.

Run npm test to execute all tests.

🤝 Contributing
Fork the repository.

Create a feature branch (git checkout -b feature/amazing-feature).

Commit your changes (git commit -m 'Add some amazing feature').

Push to the branch (git push origin feature/amazing-feature).

Open a Pull Request.

Please ensure your code adheres to the existing style and passes all tests.

📄 License
This project is licensed under the MIT License – see the LICENSE file for details.

📞 Contact
For questions or support, please contact the maintainers at dev@dhfarmer.com.

Happy farming! 🌾