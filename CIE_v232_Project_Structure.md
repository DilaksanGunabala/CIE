# CIE v2.3.2 Project Folder Structure

```
cie-v232/
│
├── README.md                           # Project overview, setup instructions
├── LICENSE
├── .gitignore
├── .env.example                        # Environment variable template
├── docker-compose.yml                  # Docker orchestration
├── Makefile                            # Common commands (migrate, seed, test)
│
├── docs/                               # Documentation
│   ├── api/
│   │   ├── openapi.yaml               # API specification
│   │   └── postman_collection.json    # API testing collection
│   ├── architecture/
│   │   ├── system_design.md           # High-level architecture
│   │   ├── database_schema.md         # DB schema documentation
│   │   └── data_flow_diagrams/        # System flow charts
│   ├── user_guides/
│   │   ├── content_editor_guide.md
│   │   ├── seo_governor_guide.md
│   │   └── admin_guide.md
│   └── deployment/
│       ├── deployment_guide.md
│       ├── runbook.md                 # Operations manual
│       └── disaster_recovery.md
│
├── config/                             # Configuration files
│   ├── database.php                   # Database connection config
│   ├── redis.php                      # Redis cache config
│   ├── api.php                        # API settings
│   ├── mail.php                       # Email/SMTP config
│   └── constants.php                  # System-wide constants
│
├── database/                           # Database management
│   ├── migrations/
│   │   ├── 001_create_users_table.sql
│   │   ├── 002_create_roles_table.sql
│   │   ├── 003_create_skus_table.sql
│   │   ├── 004_create_clusters_table.sql
│   │   ├── 005_create_intents_table.sql
│   │   ├── 006_create_sku_intents_table.sql
│   │   ├── 007_create_audit_results_table.sql
│   │   ├── 008_create_content_briefs_table.sql
│   │   ├── 009_create_validation_logs_table.sql
│   │   ├── 010_create_tier_history_table.sql
│   │   ├── 011_create_cluster_vectors_table.sql
│   │   ├── 012_create_sku_vectors_table.sql
│   │   ├── 013_create_channel_mappings_table.sql
│   │   ├── 014_create_audit_log_table.sql
│   │   └── 015_create_erp_sync_log_table.sql
│   ├── seeds/
│   │   ├── 001_seed_intents.sql       # 9 locked intents
│   │   ├── 002_seed_tiers.sql         # 4 tier types
│   │   ├── 003_seed_roles.sql         # 9 RBAC roles
│   │   ├── 004_seed_test_users.sql    # Dev/staging users
│   │   └── 005_seed_golden_test_data.sql  # From golden_test_data.json
│   └── schema/
│       └── cie_cable_canonical_schema.csv  # Field definitions (from Excel)
│
├── backend/                            # Backend API (PHP/Python hybrid)
│   │
│   ├── php/                           # PHP components
│   │   ├── public/
│   │   │   └── index.php              # Entry point
│   │   ├── src/
│   │   │   ├── Controllers/
│   │   │   │   ├── AuthController.php
│   │   │   │   ├── SkuController.php
│   │   │   │   ├── ClusterController.php
│   │   │   │   ├── ValidationController.php
│   │   │   │   ├── AuditController.php
│   │   │   │   ├── BriefController.php
│   │   │   │   ├── TierController.php
│   │   │   │   └── UserController.php
│   │   │   ├── Models/
│   │   │   │   ├── Sku.php
│   │   │   │   ├── Cluster.php
│   │   │   │   ├── Intent.php
│   │   │   │   ├── SkuIntent.php
│   │   │   │   ├── AuditResult.php
│   │   │   │   ├── ContentBrief.php
│   │   │   │   ├── User.php
│   │   │   │   ├── Role.php
│   │   │   │   └── ValidationLog.php
│   │   │   ├── Services/
│   │   │   │   ├── TierCalculationService.php
│   │   │   │   ├── ValidationService.php
│   │   │   │   ├── IntentAssignmentService.php
│   │   │   │   ├── ReadinessScoreService.php
│   │   │   │   ├── ERPSyncService.php
│   │   │   │   └── NotificationService.php
│   │   │   ├── Middleware/
│   │   │   │   ├── AuthMiddleware.php
│   │   │   │   ├── RBACMiddleware.php
│   │   │   │   ├── TierLockMiddleware.php
│   │   │   │   ├── RateLimitMiddleware.php
│   │   │   │   └── LoggingMiddleware.php
│   │   │   ├── Validators/
│   │   │   │   ├── Gates/
│   │   │   │   │   ├── G1_BasicInfoGate.php
│   │   │   │   │   ├── G2_ImagesGate.php
│   │   │   │   │   ├── G3_SEOGate.php
│   │   │   │   │   ├── G4_VectorGate.php
│   │   │   │   │   ├── G5_TechnicalGate.php
│   │   │   │   │   ├── G6_CommercialGate.php
│   │   │   │   │   └── G7_ExpertGate.php
│   │   │   │   ├── GateValidator.php      # Orchestrates all gates
│   │   │   │   └── SchemaValidator.php    # Field-level validation
│   │   │   ├── Enums/
│   │   │   │   ├── TierType.php
│   │   │   │   ├── GateType.php
│   │   │   │   ├── ValidationStatus.php
│   │   │   │   ├── IntentType.php
│   │   │   │   ├── AuditEngineType.php
│   │   │   │   └── RoleType.php
│   │   │   ├── Utils/
│   │   │   │   ├── Logger.php
│   │   │   │   ├── CacheManager.php
│   │   │   │   ├── FileUploader.php
│   │   │   │   └── ResponseFormatter.php
│   │   │   └── Database/
│   │   │       └── Connection.php
│   │   ├── routes/
│   │   │   ├── api.php                # API route definitions
│   │   │   └── web.php                # Web routes (if any)
│   │   ├── tests/
│   │   │   ├── Unit/
│   │   │   │   ├── TierCalculationTest.php
│   │   │   │   ├── ValidationTest.php
│   │   │   │   └── RBACTest.php
│   │   │   └── Integration/
│   │   │       ├── EndToEndTest.php
│   │   │       └── GateEnforcementTest.php
│   │   ├── composer.json
│   │   └── composer.lock
│   │
│   └── python/                        # Python components (vector, AI)
│       ├── src/
│       │   ├── vector/
│       │   │   ├── __init__.py
│       │   │   ├── cluster_cache.py   # Redis/DB/memory cache (YOUR CODE)
│       │   │   ├── embedding.py       # OpenAI embeddings + similarity (YOUR CODE)
│       │   │   └── validation.py      # validate_cluster_match function
│       │   ├── ai_audit/
│       │   │   ├── __init__.py
│       │   │   ├── audit_engine.py    # Multi-engine orchestration
│       │   │   ├── engines/
│       │   │   │   ├── perplexity_engine.py
│       │   │   │   ├── openai_engine.py
│       │   │   │   ├── anthropic_engine.py
│       │   │   │   └── gemini_engine.py
│       │   │   └── decay_detector.py  # Detect 3-week decay patterns
│       │   ├── brief_generator/
│       │   │   ├── __init__.py
│       │   │   ├── generator.py       # Auto-generate content briefs
│       │   │   └── templates.py       # Brief templates
│       │   ├── erp_sync/
│       │   │   ├── __init__.py
│       │   │   ├── sync_job.py        # Nightly ERP sync
│       │   │   ├── connectors/
│       │   │   │   ├── odbc_connector.py
│       │   │   │   ├── rest_connector.py
│       │   │   │   └── csv_connector.py
│       │   │   └── tier_recalculator.py
│       │   ├── jobs/
│       │   │   ├── __init__.py
│       │   │   ├── nightly_erp_sync.py
│       │   │   ├── weekly_decay_check.py
│       │   │   └── vector_retry_queue.py  # Retry failed embeddings
│       │   └── utils/
│       │       ├── __init__.py
│       │       ├── logger.py
│       │       └── config.py
│       ├── tests/
│       │   ├── test_vector_validation.py
│       │   ├── test_ai_audit.py
│       │   └── test_erp_sync.py
│       ├── requirements.txt
│       ├── setup.py
│       └── README.md
│
├── frontend/                           # Frontend application
│   ├── public/
│   │   ├── index.html
│   │   ├── favicon.ico
│   │   └── assets/
│   │       ├── images/
│   │       └── icons/
│   ├── src/
│   │   ├── components/
│   │   │   ├── common/
│   │   │   │   ├── Header.jsx
│   │   │   │   ├── Sidebar.jsx
│   │   │   │   ├── Footer.jsx
│   │   │   │   ├── Button.jsx
│   │   │   │   ├── Input.jsx
│   │   │   │   ├── Modal.jsx
│   │   │   │   └── Toast.jsx
│   │   │   ├── sku/
│   │   │   │   ├── SkuList.jsx        # SKU listing table
│   │   │   │   ├── SkuEditForm.jsx    # Main edit form (tier badges, locks)
│   │   │   │   ├── SkuDetailView.jsx
│   │   │   │   ├── TierBadge.jsx      # Hero/Support/Harvest/Kill badge
│   │   │   │   ├── TierLockBanner.jsx # "Fields locked" warning
│   │   │   │   ├── ValidationPanel.jsx # Shows gate results
│   │   │   │   └── ImageUploader.jsx  # Drag-drop image upload
│   │   │   ├── cluster/
│   │   │   │   ├── ClusterList.jsx
│   │   │   │   ├── ClusterEditForm.jsx
│   │   │   │   ├── ClusterApprovalQueue.jsx  # SEO Governor approval
│   │   │   │   └── IntentViewer.jsx
│   │   │   ├── audit/
│   │   │   │   ├── AuditDashboard.jsx # AI audit results
│   │   │   │   ├── AuditScoreCard.jsx # Per-engine breakdown
│   │   │   │   └── DecayMonitor.jsx   # Risk SKU list
│   │   │   ├── brief/
│   │   │   │   ├── BriefQueue.jsx     # Content Lead view
│   │   │   │   ├── BriefDetailModal.jsx
│   │   │   │   └── EffortReport.jsx   # Hours logged
│   │   │   ├── dashboard/
│   │   │   │   ├── AdminDashboard.jsx
│   │   │   │   ├── ContentDashboard.jsx
│   │   │   │   ├── SEODashboard.jsx
│   │   │   │   └── ReadinessWidget.jsx
│   │   │   └── auth/
│   │   │       ├── Login.jsx
│   │   │       └── UserProfile.jsx
│   │   ├── pages/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── SKUs.jsx
│   │   │   ├── Clusters.jsx
│   │   │   ├── Audits.jsx
│   │   │   ├── Briefs.jsx
│   │   │   └── Settings.jsx
│   │   ├── hooks/
│   │   │   ├── useAuth.js
│   │   │   ├── useValidation.js
│   │   │   ├── useTierLock.js
│   │   │   └── useRBAC.js
│   │   ├── services/
│   │   │   ├── api.js                 # Axios instance
│   │   │   ├── skuService.js
│   │   │   ├── clusterService.js
│   │   │   ├── validationService.js
│   │   │   ├── auditService.js
│   │   │   └── authService.js
│   │   ├── store/                     # State management (Redux/Zustand)
│   │   │   ├── index.js
│   │   │   ├── slices/
│   │   │   │   ├── authSlice.js
│   │   │   │   ├── skuSlice.js
│   │   │   │   ├── clusterSlice.js
│   │   │   │   └── uiSlice.js
│   │   │   └── middleware/
│   │   │       └── apiMiddleware.js
│   │   ├── utils/
│   │   │   ├── constants.js           # Frontend constants
│   │   │   ├── validators.js          # Client-side validation
│   │   │   ├── formatters.js          # Data formatting
│   │   │   └── permissions.js         # RBAC helpers
│   │   ├── styles/
│   │   │   ├── globals.css
│   │   │   ├── variables.css
│   │   │   └── components/
│   │   │       └── [component-specific styles]
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   ├── package-lock.json
│   ├── vite.config.js                 # Or webpack/CRA config
│   └── .eslintrc.js
│
├── scripts/                            # Utility scripts
│   ├── setup/
│   │   ├── init_database.sh          # Initialize DB with migrations
│   │   ├── seed_dev_data.sh          # Load dev/staging data
│   │   └── generate_api_docs.sh      # Generate API documentation
│   ├── maintenance/
│   │   ├── backup_database.sh
│   │   ├── restore_database.sh
│   │   └── clear_cache.sh
│   ├── deployment/
│   │   ├── deploy_staging.sh
│   │   ├── deploy_production.sh
│   │   └── rollback.sh
│   └── testing/
│       ├── run_all_tests.sh
│       ├── run_golden_tests.sh       # golden_test_data.json validation
│       └── load_test.sh
│
├── jobs/                              # Scheduled jobs (cron)
│   ├── nightly_erp_sync.sh           # Wrapper for Python ERP sync
│   ├── weekly_decay_check.sh         # Wrapper for decay detector
│   ├── hourly_vector_retry.sh        # Retry failed embeddings
│   └── daily_backup.sh
│
├── infrastructure/                    # Infrastructure as Code
│   ├── docker/
│   │   ├── Dockerfile.php            # PHP-FPM container
│   │   ├── Dockerfile.python         # Python worker container
│   │   ├── Dockerfile.nginx          # Nginx reverse proxy
│   │   └── nginx.conf
│   ├── kubernetes/                    # K8s manifests (if using K8s)
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   ├── ingress.yaml
│   │   └── configmap.yaml
│   └── terraform/                     # Cloud infrastructure (if using Terraform)
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
│
├── monitoring/                        # Observability
│   ├── prometheus/
│   │   └── prometheus.yml
│   ├── grafana/
│   │   └── dashboards/
│   │       ├── cie_system_health.json
│   │       ├── gate_validation_metrics.json
│   │       └── tier_distribution.json
│   └── logs/
│       └── .gitkeep                  # Logs written here by app
│
├── tests/                             # Integration & E2E tests
│   ├── integration/
│   │   ├── test_full_pipeline.py     # ERP → Tier → Validation → Publish
│   │   ├── test_gate_enforcement.py
│   │   └── test_rbac_restrictions.py
│   ├── e2e/
│   │   ├── cypress/                  # Or Playwright
│   │   │   ├── fixtures/
│   │   │   │   └── golden_test_data.json
│   │   │   ├── integration/
│   │   │   │   ├── sku_edit_flow.spec.js
│   │   │   │   ├── validation_flow.spec.js
│   │   │   │   └── tier_lock_flow.spec.js
│   │   │   └── support/
│   │   │       └── commands.js
│   │   └── cypress.config.js
│   └── load/
│       └── locustfile.py             # Load testing with Locust
│
├── cache/                             # Application cache
│   ├── vectors/                      # Cluster vector cache (if file-based)
│   └── .gitkeep
│
└── storage/                           # File storage
    ├── uploads/
    │   ├── images/                   # SKU images
    │   └── erp_files/                # ERP CSV/XML drops
    └── exports/
        └── audit_reports/            # Generated reports

```

---

## Key Directory Details

### Backend PHP Structure
- **Controllers**: Handle HTTP requests, route to services
- **Models**: Database entities (Eloquent ORM or similar)
- **Services**: Business logic (tier calculation, validation)
- **Validators/Gates**: Each gate is a separate class (G1-G7)
- **Middleware**: Auth, RBAC, tier-lock enforcement, logging
- **Enums**: Type-safe enums for tiers, gates, statuses

### Backend Python Structure
- **vector/**: Your cluster cache + embedding code
- **ai_audit/**: Multi-engine audit system (4 LLM APIs)
- **brief_generator/**: Auto-generate content briefs
- **erp_sync/**: Nightly sync job with multiple connectors
- **jobs/**: Scheduled background tasks

### Frontend Structure
- **components/sku/**: SKU edit form with tier badges and locks
- **components/audit/**: Decay monitor, AI audit dashboard
- **components/brief/**: Brief queue for Content Leads
- **hooks/**: Reusable React hooks (useAuth, useTierLock, etc.)
- **services/**: API client wrappers
- **store/**: Global state (user, SKUs, validation results)

### Database Migrations
- Sequential numbered migrations (001-015)
- Seed files for locked intents, tiers, roles
- Golden test data seeding for validation

### Jobs/Cron
- **Nightly**: ERP sync + tier recalculation
- **Weekly**: Decay detection + brief generation
- **Hourly**: Retry failed vector embeddings

---

## Environment Variables (.env.example)

```bash
# Application
APP_ENV=production
APP_DEBUG=false
APP_URL=https://cie.yourcompany.com

# Database
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=cie_v232
DB_USERNAME=cie_user
DB_PASSWORD=your_secure_password

# Redis (vector cache)
REDIS_URL=redis://localhost:6379/0

# OpenAI (embeddings)
OPENAI_API_KEY=sk-...

# AI Audit Engines
PERPLEXITY_API_KEY=pplx-...
ANTHROPIC_API_KEY=sk-ant-...
GEMINI_API_KEY=...

# ERP Integration
ERP_CONNECTION_STRING=Driver={SQL Server};Server=erp.company.com;Database=ProductDB;
ERP_SYNC_ENABLED=true
ERP_SYNC_SCHEDULE=0 2 * * *  # 2 AM daily

# Email/SMTP
MAIL_MAILER=smtp
MAIL_HOST=smtp.company.com
MAIL_PORT=587
MAIL_USERNAME=cie@company.com
MAIL_PASSWORD=...
MAIL_FROM_ADDRESS=cie@company.com
MAIL_FROM_NAME="CIE System"

# Vector Validation
SIMILARITY_THRESHOLD=0.72
EMBEDDING_TIMEOUT=3000  # milliseconds
VECTOR_CACHE_TTL=86400  # 24 hours

# Feature Flags
FAIL_SOFT_ENABLED=true
DECAY_MONITORING_ENABLED=true
AUTO_BRIEF_GENERATION=true

# Logging
LOG_LEVEL=info
LOG_CHANNEL=stack
```

---

## Package Dependencies

### PHP (composer.json)
```json
{
  "require": {
    "php": "^8.1",
    "guzzlehttp/guzzle": "^7.5",
    "league/fractal": "^0.20",
    "vlucas/phpdotenv": "^5.5",
    "respect/validation": "^2.2",
    "predis/predis": "^2.1",
    "monolog/monolog": "^3.3"
  },
  "require-dev": {
    "phpunit/phpunit": "^10.0",
    "mockery/mockery": "^1.5",
    "fakerphp/faker": "^1.21"
  }
}
```

### Python (requirements.txt)
```
openai==1.12.0
anthropic==0.18.0
google-generativeai==0.3.2
numpy==1.26.4
redis==5.0.1
requests==2.31.0
python-dotenv==1.0.1
pandas==2.2.0
psycopg2-binary==2.9.9
pymysql==1.1.0
schedule==1.2.0
pytest==8.0.0
```

### Frontend (package.json)
```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.22.0",
    "axios": "^1.6.7",
    "zustand": "^4.5.0",
    "react-hook-form": "^7.50.0",
    "react-dropzone": "^14.2.3",
    "recharts": "^2.12.0",
    "date-fns": "^3.3.1",
    "clsx": "^2.1.0"
  },
  "devDependencies": {
    "vite": "^5.1.0",
    "cypress": "^13.6.4",
    "eslint": "^8.56.0",
    "prettier": "^3.2.5"
  }
}
```

---

## Critical Files Summary

| File | Purpose | Owner |
|------|---------|-------|
| `backend/python/src/vector/cluster_cache.py` | Redis/DB/memory cache | YOUR EARLIER CODE |
| `backend/python/src/vector/embedding.py` | OpenAI embeddings + cosine similarity | YOUR EARLIER CODE |
| `backend/python/src/vector/validation.py` | validate_cluster_match function | YOUR EARLIER CODE |
| `backend/php/src/Validators/Gates/G4_VectorGate.php` | Calls Python vector validation | NEW - integrates your code |
| `backend/php/src/Services/TierCalculationService.php` | Computes Hero/Support/Harvest/Kill | CRITICAL |
| `backend/php/src/Middleware/TierLockMiddleware.php` | Enforces field locks per tier | CRITICAL |
| `backend/python/src/ai_audit/audit_engine.py` | Multi-LLM audit orchestration | CRITICAL |
| `backend/python/src/erp_sync/sync_job.py` | Nightly ERP sync | CRITICAL |
| `frontend/src/components/sku/SkuEditForm.jsx` | Main edit UI with tier badges | CRITICAL |

---

This structure supports:
- ✅ Microservices architecture (PHP API + Python workers)
- ✅ Clear separation of concerns
- ✅ Your existing vector validation code
- ✅ All 15 build steps from the implementation guide
- ✅ RBAC enforcement at middleware level
- ✅ Scheduled jobs for automation
- ✅ Comprehensive testing (unit, integration, E2E)
- ✅ Production-ready deployment
