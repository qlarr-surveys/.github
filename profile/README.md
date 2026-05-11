# Qlarr

[![Discord](https://img.shields.io/discord/YOUR_DISCORD_ID?color=7289da&label=Discord&logo=discord&logoColor=white)](https://discord.gg/3exUNKwsET)

**Qlarr** is an open-source framework for creating and running customizable, scientific, and offline-first surveys as code on all platforms. Surveys are defined using JSON to represent UI-agnostic survey components and JavaScript instructions to represent complex survey logic.

## 🌟 Key Features

- **📴 Offline-First Design** - Collect data anywhere without internet connectivity
- **⍰ Conditional Logic & Skip Logic** - Advanced branching based on user responses
- **✅ Input Validation** - Ensure data quality with built-in validation checks
- **🎲 Randomization & Sampling** - Randomize questions and options with weighted priorities
- **🌐 Multilingual Surveys** - Support for multiple languages
- **🔗 Piping** - Reference and display values from previous answers
- **⬅️➡️ Flexible Navigation** - All questions, page-by-page, or question-by-question
- **⏱️ Time Limits & 📊 Scoring** (WIP) - Perfect for quizzes and timed assessments
- **🎨 Conditional Formatting** (WIP) - Dynamic styling based on responses

## 🏗️ Architecture

The Qlarr ecosystem consists of four main components:

### 1. [Survey Engine (KMP)](https://github.com/qlarr-surveys/survey-engine-kmp)
The core UI-agnostic engine that powers all survey functionality. Written in Kotlin JVM with plans to migrate to Kotlin Native for cross-platform support.

**What it does:**
- Parses survey definitions (JSON + JavaScript) into a component graph
- Generates state machine files for UI interactions
- Creates database schemas for response storage
- Validates survey structure and logic
- Manages survey execution and state updates

**Two Main Use Cases:**
1. **Processing Survey Design** → Generates component graph, state machine resources, DB schema, and validated design
2. **Running Surveys** → Takes processed survey + user responses → Generates reduced survey, state machine, and values to save

### 2. [Survey Engine Script](https://github.com/qlarr-surveys/survey-engine-script)
A JavaScript validation library for dynamic survey instructions.

**What it does:**
- Parses JavaScript expressions into Abstract Syntax Trees (AST)
- Validates survey logic against safety rules
- Prevents dangerous operations (variable declarations, loops, assignments)
- Allows safe operations (conditionals, math, object/array expressions, function calls)
- Whitelists accessible variables and methods

**Example Valid Instructions:**
```javascript
Q1.relevance && Q1.value
Q2.value > 100 ? "High" : "Low"
Math.abs(Q3.value - Q4.value)
"Hello " + userName
```

### 3. [Backend](https://github.com/qlarr-surveys/backend)
Spring Boot application serving as the backend core (nicknamed "Frankie Backend Core").

**What it does:**
- Exposes REST APIs for creating and executing surveys
- Supports offline survey caching and response syncing
- Manages survey CRUD operations
- Handles authentication and user management
- Provides administrative functionalities

**Tech Stack:**
- Java 19+ / Spring Boot
- PostgreSQL database
- Docker support for easy deployment

### 4. [Frontend](https://github.com/qlarr-surveys/frontend)
React-based web application providing the user interface.

**What it does:**
- WYSIWYG survey editor for creating and editing surveys
- Renders surveys powered by the Survey Engine
- Provides GUI for survey management
- Handles user authentication and administrative tasks

**Tech Stack:**
- React
- Node.js
- Environment-based configuration

## 🚀 Quick Start

### Using Docker (Recommended for Production)

```bash
# Clone the backend repository
git clone https://github.com/qlarr-surveys/backend.git
cd backend

# Deploy both frontend and backend
docker-compose up
```

### Local Development

#### Backend
```bash
# Prerequisites: Java 19+, Docker (optional for database)

git clone https://github.com/qlarr-surveys/backend.git
cd backend

# Start PostgreSQL (with Docker)
docker-compose up -d postgres-db

# Build and run
./gradlew build
./gradlew bootRun

# Access at http://localhost:8080
```

#### Frontend
```bash
# Prerequisites: Node.js

git clone https://github.com/qlarr-surveys/frontend.git
cd frontend

# Install dependencies
npm install

# Configure environment
# Edit .env file with API endpoints

# Run development server
npm run start

# Access at http://localhost:3000
```

#### Survey Engine Script
```bash
git clone https://github.com/qlarr-surveys/survey-engine-script.git
cd survey-engine-script

npm install

# Add tests to tests/index.test.js
npm test

# Build
npm run build
```

## 📊 How It Works

1. **Design Phase**: Use the frontend WYSIWYG editor to create surveys with:
   - Questions defined in JSON
   - Logic defined in JavaScript expressions
   - Validation and conditional branching

2. **Processing Phase**: Survey Engine validates and processes the design:
   - Creates component graph
   - Generates state machine
   - Produces database schema

3. **Execution Phase**: Survey Engine manages survey runtime:
   - Applies conditional logic
   - Handles navigation
   - Updates state based on user input
   - Saves responses

4. **Data Collection**: Backend manages:
   - Online/offline synchronization
   - Response storage
   - Survey distribution

## 🛠️ Development

### Running Tests

**Backend:**
```bash
./gradlew test
```

**Frontend:**
```bash
npm test
```

**Survey Engine Script:**
```bash
npm test
```

## 🤝 Contributing

We welcome contributors! The easiest way to get involved:

1. Join our [Discord server](https://discord.gg/3exUNKwsET) and talk to us directly
2. For new features: Start a Discussion/Idea
3. For bugs: Raise an issue with clear reproduction steps
4. Export the survey with the issue and include it in your bug report

## 🗺️ Roadmap

- [ ] Complete time limits and scoring features for quizzes
- [ ] Implement conditional formatting
- [ ] Migrate Survey Engine to Kotlin Native for Node.js and iOS support
- [ ] Enhanced mobile applications (Android, iOS)
- [ ] Additional question types and validation methods

## 📄 License

Open-source - check individual repositories for specific license information.

## 🔗 Resources

- **Website**: [https://www.qlarr.com](https://www.qlarr.com)
- **Discord**: [Join our community](https://discord.gg/3exUNKwsET)
- **Documentation**: https://qlarr-surveys.github.io/docs/

## 📱 Platform Support

- ✅ Web (Frontend + Backend)
- ✅ Android (using Survey Engine KMP)
- 🔄 iOS (planned with Kotlin Native migration)
- 🔄 Node.js backend (planned with Kotlin Native migration)

---

**Built with ❤️ by the Qlarr Surveys community**
