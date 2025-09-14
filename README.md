# Frauddi API Documentation

<p align="center">
  <img src="static/logo/logo.png" alt="Frauddi Logo">
  <br>
  <a href="https://docs.frauddi.com"><img src="https://img.shields.io/badge/docs-live-brightgreen" alt="Documentation"></a>
  <a href="https://api.frauddi.com"><img src="https://img.shields.io/badge/API-production-blue" alt="API Status"></a>
</p>

<p align="center">Official REST API for Frauddi fraud detection platform</p>

## About

The Frauddi API is organized around REST with predictable resource-oriented URLs, JSON-encoded request bodies, and standard HTTP response codes. Our API provides programmatic access to fraud detection, rule management, entity relationship mapping, and operational analytics.

**Base URL:** `https://api.frauddi.com`

## Core Capabilities

- **Risk Assessment** - Real-time fraud scoring for transactions and users
- **Rule Management** - Custom fraud detection rule configuration
- **Graph Analysis** - Entity relationship mapping and network analysis
- **Analytics** - Event aggregation and pattern analysis
- **Entity Management** - Blacklist and whitelist operations
- **System Monitoring** - Health checks and operational status

## Authentication

All API requests require authentication using your API key in the Authorization header:

```bash
Authorization: Bearer your_api_key_here
```

## Getting Your API Key

Contact our sales team or access your Frauddi dashboard to obtain your API key:

- **Email:** [sales@frauddi.com](mailto:sales@frauddi.com)
- **Support:** [support@frauddi.com](mailto:support@frauddi.com)

## Documentation

Complete interactive API documentation: **[docs.frauddi.com](https://docs.frauddi.com)**

## Quick Start

1. Obtain your API key from our sales team or dashboard
2. Make a test request to `/ping` endpoint
3. Submit transaction data to `/assessments/` endpoints
4. Configure detection rules via `/rules/` endpoints

## Response Format

All API responses use standard HTTP status codes and return JSON-encoded data with consistent error handling.

## Support

- **Technical Support:** [support@frauddi.com](mailto:support@frauddi.com)
- **Sales Inquiries:** [sales@frauddi.com](mailto:sales@frauddi.com)
- **Website:** [frauddi.com](https://frauddi.com)

## Auto-Generated Documentation

This documentation automatically updates from our OpenAPI specification every 6 hours using GitHub Actions.

---

Built with ❤️ by the Frauddi team
