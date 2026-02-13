# CIE v2.3.2 - Catalog Intelligence Engine

## Overview
CIE is an enterprise-grade product content management system with AI-powered validation, tier-based governance, and automated quality enforcement.

## Tech Stack
- **Backend**: PHP 8.1+ (Laravel/Custom), Python 3.11+ (FastAPI/Flask)
- **Frontend**: React 18.2+, Zustand, Axios
- **Database**: MySQL 8.0 / PostgreSQL 14+
- **Cache**: Redis 7.0+
- **Infrastructure**: Docker, Nginx

## Setup
1. Clone the repository.
2. Copy `.env.example` to `.env` and configure your API keys.
3. Run `docker-compose up -d`.
4. Run `make migrate` and `make seed`.
5. Start frontend: `cd frontend && npm install && npm run dev`.

## Documentation
Refer to the `docs/` folder for detailed guides and API specifications.
