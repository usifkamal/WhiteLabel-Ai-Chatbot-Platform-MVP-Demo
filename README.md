# White-Label AI Chatbot Platform MVP - Demo Version

> **🎭 Demo Version**: This is a **demo version** of the White-Label AI Chatbot Platform, configured with demo mode enabled by default. Perfect for showcasing to clients without connecting to real databases or storing real data.

A comprehensive monorepo containing two main services for building a white-label AI chatbot platform:

- **Backend** (`/backend`) - File processing, URL crawling, document management, and AI embeddings service
- **Frontend** (`/frontend`) - User interface, dashboard, and chat experience

## 🎭 Demo Mode Features

This demo version includes:

- ✅ **Demo Mode Enabled**: Mock data instead of real database connections
- ✅ **Authentication Disabled**: No sign-in/up required for testing
- ✅ **Demo Banner**: Clear indicator that you're in demo mode
- ✅ **Mock Data**: Pre-configured demo tenant, chats, and analytics
- ✅ **Safe for Clients**: No real data is stored or accessed

**To enable demo mode:**
1. Set `DEMO_MODE=true` and `NEXT_PUBLIC_DEMO_MODE=true` in `frontend/.env.local`
2. Restart the development server
3. See [ENABLE_DEMO_MODE.md](frontend/ENABLE_DEMO_MODE.md) for detailed instructions

**Note:** This demo version does not connect to real databases or store real data. Perfect for client demonstrations!

## 🏗️ Architecture

This monorepo uses **pnpm workspaces** to manage two independent Next.js applications:

```
├── backend/          # File processing & ingestion service (Port 3004)
├── frontend/         # Chat UI & dashboard service (Port 3000)
├── package.json      # Root workspace configuration
└── README.md
```

## 🌍 EU Compliance

This platform is configured for EU compliance with:
- **Supabase Region**: Frankfurt (EU Central 1)
- **No Telemetry**: All tracking and analytics disabled
- **GDPR Compliant**: Full data protection compliance
- **EU-Based Infrastructure**: All data processing within EU

See [EU Compliance Documentation](docs/EU-COMPLIANCE.md) and [GDPR Checklist](docs/GDPR.md) for details.

## 🚀 Quick Start

### Prerequisites

- **Node.js** >= 18.0.0
- **pnpm** >= 8.0.0
- **Supabase** account and project (Frankfurt region)
- **OpenAI** API key

### Installation

1. **Clone and install dependencies:**
   ```bash
   git clone <your-repo-url>
   cd white-label-ai-chatbot-platform
   pnpm install
   ```

2. **Set up environment variables:**
   
   Copy the example environment files and configure them:
   ```bash
   cp docs/env-examples/backend.env.example backend/.env.local
   cp docs/env-examples/frontend.env.example frontend/.env.local
   ```

3. **Configure each service:**
   
   **Backend** (`backend/.env.local`):
   ```env
   # Supabase Configuration
   NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
   
   # AI Services
   GEMINI_API_KEY=your_gemini_api_key
   OPENAI_API_KEY=your_openai_api_key
   
   # Application
   PORT=3004
   NEXT_TELEMETRY_DISABLED=1
   ```

   **Frontend** (`frontend/.env.local`):
   ```env
   # Supabase Configuration
   NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
   
   # AI Services
   GEMINI_API_KEY=your_gemini_api_key
   OPENAI_API_KEY=your_openai_api_key
   
   # Application
   NEXT_PUBLIC_BACKEND_URL=http://localhost:3004
   NEXT_TELEMETRY_DISABLED=1
   ```

### Running the Services

#### Option 1: Run All Services (Recommended)
```bash
# Start all services in parallel
pnpm dev
```

This will start:
- Backend: http://localhost:3004
- Frontend: http://localhost:3000

#### Option 2: Run Individual Services
```bash
# Backend only
pnpm --filter backend run dev

# Frontend only
pnpm --filter frontend run dev
```

## 📁 Project Structure

### Backend (`/backend`)
- **Purpose**: File processing, URL crawling, document management, and AI embeddings
- **Tech Stack**: Next.js 15, Supabase, Gemini/OpenAI, TypeScript, Langchain
- **Key Features**:
  - File upload and processing (PDF, TXT)
  - URL crawling and content extraction (Cheerio)
  - Document chunking and embedding (Gemini)
  - Vector search capabilities (pgvector)
  - Background job processing
  - Multi-tenant API with authentication

### Frontend (`/frontend`)
- **Purpose**: User interface and chat experience
- **Tech Stack**: Next.js 13, React, Tailwind CSS, TypeScript
- **Key Features**:
  - Modern chat interface
  - Real-time messaging
  - User authentication
  - Responsive design

## 🛠️ Development Commands

### Root Level Commands
```bash
# Install all dependencies
pnpm install

# Run all services in development
pnpm dev

# Build all services
pnpm build

# Start all services in production
pnpm start

# Lint all services
pnpm lint

# Type check all services
pnpm type-check

# Clean all node_modules
pnpm clean
```

### Service-Specific Commands
```bash
# Backend commands
pnpm --filter backend run dev
pnpm --filter backend run build
pnpm --filter backend run start


# Frontend commands
pnpm --filter frontend run dev
pnpm --filter frontend run build
```

## 🔧 Configuration

### Port Configuration
- **Backend**: 3004
- **Frontend**: 3000

### Environment Variables
Each service has its own `.env.local` file. See the `.env.example` files in each directory for required variables.

### Database Setup
1. Create a Supabase project
2. Run the migration files in each service's `supabase/migrations/` directory
3. Configure the database URLs in your environment files

## 🚀 Deployment

### Overview

This project uses a multi-service architecture:
- **Frontend**: Deploy to Vercel (Next.js optimized)
- **Backend**: Deploy to Render or Fly.io (persistent jobs, file processing)
- **Database**: Supabase (managed PostgreSQL with pgvector)

### Frontend Deployment (Vercel)

The frontend is optimized for Vercel's serverless infrastructure:

1. **Connect your repository** to Vercel
2. **Configure build settings**:
   - Root Directory: `frontend`
   - Build Command: `pnpm install && pnpm build`
   - Output Directory: `.next`
   - Install Command: `pnpm install`
3. **Set environment variables** in Vercel dashboard:
   ```
   NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
   SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
   OPENAI_API_KEY=your-openai-key
   GEMINI_API_KEY=your-gemini-key
   AUTH_SECRET=your-auth-secret
   NEXTAUTH_URL=https://your-frontend.vercel.app
   ```
4. **Deploy**: Vercel will auto-deploy on git push

### Backend Deployment (Render)

The backend requires persistent infrastructure for file processing and crawling jobs.

#### Option 1: Render (Recommended)

1. **Create a new Web Service** on Render
2. **Connect your Git repository**
3. **Configure service**:
   - **Name**: `white-label-chatbot-backend`
   - **Root Directory**: `backend`
   - **Environment**: `Node`
   - **Build Command**: `pnpm install && pnpm build`
   - **Start Command**: `pnpm start`
   - **Plan**: Starter ($7/month) or higher for production
4. **Set environment variables**:
   ```
   NODE_ENV=production
   PORT=3004
   NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
   SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
   OPENAI_API_KEY=your-openai-key
   GEMINI_API_KEY=your-gemini-key
   AUTH_SECRET=your-auth-secret
   NEXT_TELEMETRY_DISABLED=1
   MAX_FILE_SIZE=10485760
   CHUNK_SIZE=1000
   CHUNK_OVERLAP=200
   JOB_TIMEOUT_MS=300000
   ```
5. **Deploy**: Render will auto-deploy on git push

**Alternative**: Use the provided `render.yaml` for infrastructure-as-code:
```bash
# Deploy using Render CLI
render deploy
```

#### Option 2: Fly.io

1. **Install Fly CLI**: `curl -L https://fly.io/install.sh | sh`
2. **Login**: `fly auth login`
3. **Navigate to backend**: `cd backend`
4. **Launch app**: `fly launch` (uses existing `fly.toml`)
5. **Set secrets**:
   ```bash
   fly secrets set NEXT_PUBLIC_SUPABASE_URL=your-url
   fly secrets set SUPABASE_SERVICE_ROLE_KEY=your-key
   fly secrets set GEMINI_API_KEY=your-key
   # ... etc
   ```
6. **Deploy**: `fly deploy`

#### Option 3: Docker (Any Platform)

The backend includes a `Dockerfile` for containerized deployment:

1. **Build image**:
   ```bash
   cd backend
   docker build -t chatbot-backend --build-arg DOCKER_BUILD=true .
   ```

2. **Run container**:
   ```bash
   docker run -p 3004:3004 \
     -e NEXT_PUBLIC_SUPABASE_URL=your-url \
     -e SUPABASE_SERVICE_ROLE_KEY=your-key \
     chatbot-backend
   ```

3. **Deploy to any container platform**:
   - AWS ECS/Fargate
   - Google Cloud Run
   - Azure Container Instances
   - DigitalOcean App Platform

### Environment Variables Setup

#### Backend Service Variables

Create `backend/.env.local` from `backend/.env.example`:

```bash
# Core Configuration
NEXT_PUBLIC_SUPABASE_URL=https://xxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=xxx
SUPABASE_SERVICE_ROLE_KEY=xxx

# AI Services
GEMINI_API_KEY=xxx  # Required for embeddings
OPENAI_API_KEY=xxx  # Optional (for chat if not using Gemini)

# Application
PORT=3004
NODE_ENV=production
AUTH_SECRET=generate-with-openssl-rand-base64-32

# File Processing
MAX_FILE_SIZE=10485760  # 10MB
CHUNK_SIZE=1000
CHUNK_OVERLAP=200
JOB_TIMEOUT_MS=300000  # 5 minutes

# Compliance
NEXT_TELEMETRY_DISABLED=1
```

#### Frontend Service Variables

Create `frontend/.env.local` from `docs/env-examples/frontend.env.example`:

```bash
# Supabase
NEXT_PUBLIC_SUPABASE_URL=https://xxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=xxx
SUPABASE_SERVICE_ROLE_KEY=xxx

# AI Services
OPENAI_API_KEY=xxx
GEMINI_API_KEY=xxx

# Application
NEXT_PUBLIC_APP_URL=https://your-frontend.vercel.app
NEXT_PUBLIC_BACKEND_URL=https://your-backend.onrender.com
AUTH_SECRET=same-as-backend
NEXTAUTH_URL=https://your-frontend.vercel.app

# Compliance
NEXT_TELEMETRY_DISABLED=1
```

### Database Setup (Supabase)

1. **Create Supabase project** (choose Frankfurt region for EU compliance)
2. **Run migrations**:
   ```bash
   # Apply all migrations
   cd backend
   npx supabase db push
   
   # Or manually in Supabase SQL Editor:
   # Run files in order from supabase/migrations/
   ```
3. **Configure Row Level Security (RLS)**:
   - Enable RLS on all tenant-scoped tables
   - Set up policies for multi-tenancy
4. **Set up storage buckets** (if using file uploads):
   - Create bucket: `documents`
   - Set public access policies

### Post-Deployment Checklist

- [ ] Verify backend health endpoint: `https://your-backend.onrender.com/api/health`
- [ ] Test file upload: `POST /api/ingest/upload`
- [ ] Test URL crawling: `POST /api/ingest/url`
- [ ] Verify frontend can communicate with backend
- [ ] Check Supabase logs for errors
- [ ] Monitor Render/Fly.io logs for job processing
- [ ] Test authentication flow end-to-end
- [ ] Verify environment variables are set correctly
- [ ] Check CORS settings (backend should allow frontend origin)

### Background Jobs & Serverless Safety

The backend includes serverless-safe background job processing:

- **File Processing**: Runs asynchronously with timeout protection
- **URL Crawling**: Processes in background, doesn't block HTTP responses
- **Embedding Generation**: Chunked processing to avoid memory issues
- **Job Queue**: In-memory queue for job management (upgrade to Redis/BullMQ for production)

For production workloads, consider:
- **Upgrade to proper queue**: BullMQ with Redis
- **Use Supabase Queue**: Native queue service
- **Separate worker processes**: Dedicated workers for heavy processing

### Troubleshooting

#### Backend deployment issues:
- **Port conflicts**: Ensure PORT=3004 matches your platform config
- **Build failures**: Check Node.js version (18+ required)
- **Timeout errors**: Increase `JOB_TIMEOUT_MS` for large files
- **Memory issues**: Upgrade to higher tier on Render/Fly.io

#### Frontend deployment issues:
- **API errors**: Verify `NEXT_PUBLIC_BACKEND_URL` is correct
- **Auth failures**: Ensure `AUTH_SECRET` matches backend
- **CORS errors**: Check backend CORS configuration

### Production Environment

For production deployments:
1. Use **Starter plan or higher** on Render ($7+/month)
2. Enable **auto-scaling** for traffic spikes
3. Set up **monitoring** (Render/Fly.io built-in + Supabase logs)
4. Configure **backup strategy** for Supabase
5. Set up **error tracking** (Sentry, LogRocket, etc.)
6. Enable **rate limiting** via middleware
7. Use **CDN** for static assets (Vercel includes this)

### Individual Service Deployment

Each service can be deployed independently:

```bash
# Build specific service
pnpm --filter backend build
pnpm --filter frontend build
```

## 📚 Additional Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Supabase Documentation](https://supabase.com/docs)
- [Langchain Documentation](https://python.langchain.com/docs/get_started/introduction)
- [pnpm Workspaces](https://pnpm.io/workspaces)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test all services: `pnpm build && pnpm lint`
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
