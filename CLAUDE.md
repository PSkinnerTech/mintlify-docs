# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the documentation repository for Alpha School, an innovative educational platform. The documentation is built using Mintlify and covers multiple educational technology products:

- **Alpha School**: Core educational platform where students learn academics in 2 hours
- **TimeBack**: Time optimization and assessment platform with comprehensive API
- **CLR (Comprehensive Learner Record)**: Student achievement tracking system
- **QTI (Question & Test Interoperability)**: Assessment standards implementation
- **TimeBack SSO**: Single sign-on integration framework

## Development Commands

### Local Development
```bash
# Install Mintlify CLI globally
npm i -g mint

# Start local development server
mint dev

# Run on custom port
mint dev --port 3333

# Update CLI to latest version
mint update

# Validate documentation links
mint broken-links
```

### Prerequisites
- Node.js version 19 or higher
- Global Mintlify CLI installation

## Documentation Architecture

### File Structure
- `/api-reference/` - TimeBack API documentation and OpenAPI specs
- `/timeback/` - TimeBack platform guides and features
- `/tb-sso/` - Single sign-on integration documentation
- `/qti/` - QTI implementation guides
- `/clr/` - Comprehensive Learner Record documentation
- `/essentials/` - Core documentation features (code, images, navigation)
- `/ai-tools/` - AI development tool guides (Claude Code, Cursor, Windsurf)

### Configuration Files
- `docs.json` - Primary Mintlify configuration defining navigation, tabs, and structure
- `*-openapi.json` - OpenAPI specifications for API documentation
- Theme colors: Primary #007AFE, Light #40A9FF, Dark #005BB8

### API Documentation Architecture

**Hybrid Documentation System**: This project uses both OpenAPI auto-generation and custom MDX files:

1. **OpenAPI Specification**: `api-reference/timeback-openapi.json`
   - Base URL: `https://core.timebackapi.com`
   - Authentication: JWT Bearer tokens and API keys
   - Currently defines: `/results`, `/auth/me`, `/health` endpoints
   - Auto-generates interactive API playground

2. **Manual Endpoint Documentation**: `api-reference/endpoint/*.mdx`
   - Enhanced documentation with examples, use cases, and detailed explanations
   - Links to OpenAPI spec via frontmatter: `openapi: "METHOD /path"`
   - Provides richer context than auto-generated docs

**Navigation Mapping in docs.json**:
- Line 83: `"openapi": "api-reference/timeback-openapi.json"` - Auto-generates API reference
- Lines 86-108: Manual pages organized by functional groups (Student Management, Gradebook, etc.)

**IMPORTANT ISSUE**: Student management endpoints (create, read, update, delete operations) have MDX documentation but are missing from the OpenAPI specification. This creates broken `openapi:` references in the MDX frontmatter.

### Content Organization
Documentation is organized in two main tabs:
1. **Guides** - Educational content about platforms and integration
2. **API Reference** - Technical API documentation with interactive examples

Navigation is structured hierarchically with groups and pages defined in `docs.json`. OpenAPI integration automatically generates endpoint documentation from JSON specifications.

## Development Workflow

1. Make content changes to `.mdx` files
2. Test locally with `mint dev` at `http://localhost:3000`
3. Validate links with `mint broken-links`
4. Changes deploy automatically to production via GitHub integration

### API Documentation Workflow

**For New Endpoints**:
1. Add endpoint definition to `api-reference/timeback-openapi.json`
2. Create corresponding `.mdx` file in `api-reference/endpoint/`
3. Add `openapi: "METHOD /path"` to MDX frontmatter
4. Update navigation in `docs.json` if needed

**For Existing Endpoints**:
- OpenAPI changes auto-update the interactive playground
- MDX changes provide enhanced documentation and examples
- Both sources should be kept in sync for consistency

## Important Notes

- All documentation files use MDX format with Mintlify components
- API endpoints are auto-generated from OpenAPI specifications
- Local preview requires Mintlify CLI and valid `docs.json`
- Production deployment happens automatically through GitHub app integration