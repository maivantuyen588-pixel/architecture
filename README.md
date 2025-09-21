# 📈 Scoreboard API Service

## 🧩 Description

This API module powers the **scoreboard system** for the website. Its goal is to handle **user score updates** triggered by completed actions and to display the **top 10 user scores** in real-time.


## 🔧 Core Features

1. ✅ Update a user's score after completing a valid action.
2. 📡 Provide real-time leaderboard updates to all connected clients.
3. 🔐 Ensure only authenticated users can update scores.
4. ⚠️ Prevent score manipulation or abuse from malicious users.

 

## 🛠️ Tech Stack
1. ReactJS for frontend
2. NodeJS for API server, Docker deployment on AWS
3. Redis, Mysql
4. Express, Sequelize, JWT, SSE
5. Typescript, Babel, Eslint
6. ECR, ECS, Codecommit, Codebuild, RDS, API gateway, VPC, EC2, Cloudwatch


## 🔗 API Endpoints

### 1. `POST /api/v1/auth/login`

- **Description**: Accepts user's email and password to get access_token
- **Request Body**:

```json
{
  "user_email": "string",
  "password": "string"
}
```

- **Response Body**:

```json
{
  "access_token": "string"
}
```

### 2. `POST /api/v1/auth/refresh`

- **Description**: Accepts refresh token and return access_token
- **Request Body**:

```json
{
  "refresh_token": "string",
}
```
- **Response Body**:

```json
{
  "access_token": "string"
}
```

### 3. `POST /api/v1/score/update`

- **Description**: Accepts a score update request from a user after completing an action.
- **Request Body**:

```json
{
  "user_id": "string",
  "score_increase": "number"
}
```

## 🔗 Leaderboard SSE endpoint

### 1. `GET /api/v1/leaderboard/stream`

- **Description**: Get live leaderboard data
- **Request Header**: Content-Type: text/event-stream
- **Response Body**:

```json
{
  "leaderboard": []
}
```

## 🚀 Improvement


###  Rate Limiting
- Each user is limited to 1 score update per 5 seconds.
- Excessive requests will result in `429 Too Many Requests`.
- Implemented using Redis or middleware (e.g. `express-rate-limit`).


###  Scaling
- Write score to database via a queue (Kafka)
- Scale API server when there are too many request

###  Testing Strategy
- Unit Tests: mock dependency to test score validation, auth middleware, leaderboard logic.
- Integration Tests: test full API flow.
- Tools: Jest, Supertest

