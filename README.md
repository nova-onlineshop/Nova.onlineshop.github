Closest driver + lowest response time

nava/
│
├── apps/
│   ├── rider-app/        # Flutter (مسافر)
│   ├── driver-app/       # Flutter (راننده)
│
├── backend/
│   ├── api/              # NestJS / Django
│   ├── modules/
│   │   ├── auth/
│   │   ├── rides/
│   │   ├── drivers/
│   │   ├── payments/
│   │   ├── wallet/
│   │
│   ├── prisma/ or models/
│   ├── config/
│   └── main.ts / app.py
│
├── infra/
│   ├── docker/
│   ├── nginx/
│   ├── ci-cd/
│
├── docs/
│   ├── architecture.md
│   ├── api-spec.md
│   ├── database-schema.md
│   ├── pitch-deck.md
│
├── scripts/
│   ├── seed-db.js
│   ├── deploy.sh
│
└── README.md

POST /auth/login
POST /auth/verify-otp
POST /auth/logout

POST /rides/request
GET  /rides/:id
POST /rides/:id/accept
POST /rides/:id/start
POST /rides/:id/end

POST /drivers/register
GET  /drivers/nearby
POST /drivers/go-online
POST /drivers/go-offline

POST /payments/initiate
POST /payments/confirm
GET  /payments/history

GET  /wallet/balance
POST /wallet/topup
POST /wallet/withdraw

id UUID PRIMARY KEY
phone VARCHAR UNIQUE
role ENUM('rider','driver')
created_at TIMESTAMP

id UUID PRIMARY KEY
user_id UUID
vehicle_type VARCHAR
rating FLOAT
is_online BOOLEAN
current_location GEOGRAPHY

id UUID PRIMARY KEY
rider_id UUID
driver_id UUID
status ENUM('requested','accepted','started','completed','cancelled')
price FLOAT
distance FLOAT
created_at TIMESTAMP

id UUID
ride_id UUID
amount FLOAT
method ENUM('cash','mpesa','wallet')
status ENUM('pending','paid','failed')

id UUID
user_id UUID
balance FLOAT

lib/
├── core/
│   ├── network/
│   ├── utils/
│   ├── constants/
│
├── features/
│   ├── auth/
│   ├── map/
│   ├── rides/
│   ├── wallet/
│
├── shared/
│   ├── widgets/
│   ├── models/
│
└── main.dart

HomeScreen → Select Destination → Ride Options → Confirm Ride → Live Tracking → Rating

Login → Go Online → Receive Request → Accept → Navigate → Complete Ride → Earnings

driver_location_update
ride_request
ride_accepted
ride_started
ride_completed

POST /mpesa/stkpush
POST /mpesa/callback

name: Nava CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install backend
        run: npm install
      - name: Run tests
        run: npm test

# Nava 🚗💳

Nava is a mobility + financial super-app for emerging markets.

## Features
- Ride hailing
- Driver app
- Wallet system
- M-Pesa integration

## Tech Stack
- Flutter
- Node.js (NestJS)
- PostgreSQL
- Redis
- WebSockets

## Status
MVP Development Phase

