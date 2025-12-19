---
description: Check and display project status
argument-hint: [service]
---

# /status

## Purpose
Check and display comprehensive project status including services, deployments, and health metrics.

## Contract
**Inputs:**
- `$1` — SERVICE (optional) - Specific service to check (api, database, frontend, all)

**Outputs:**
- Overall system status
- Individual service statuses
- Recent deployment information
- Performance metrics
- Active issues or alerts

## Instructions
1. If no service specified, check all services
2. For each service, verify:
   - Health endpoint response
   - Resource utilization (CPU, memory)
   - Last successful deployment
   - Error rates
3. Compile status report with:
   - Overall status (healthy/degraded/down)
   - Service-specific details
   - Recommended actions if issues found
4. Format output in readable format

## Service Checks
- **api**: REST API health, response times, error rates
- **database**: Connection status, query performance
- **frontend**: Build status, CDN health
- **all**: Complete system overview (default)

## Status Indicators
- ✅ Healthy - All systems operational
- ⚠️ Degraded - Some issues but functional
- ❌ Down - Service unavailable

## Examples
- `/status` → Show all services status
- `/status api` → Check only API service
- `/status database` → Check database status