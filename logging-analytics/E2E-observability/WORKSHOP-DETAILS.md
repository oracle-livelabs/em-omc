# Workshop Details

Estimated Time: 5 minutes

## Short Description

Deploy OCTO APM Demo and use seven OCI Observability and Management services to investigate application behavior across Kubernetes, security, distributed traces, and Oracle Database.

## Long Description

This workshop helps customers understand end-to-end observability for applications running on OCI or connected from other environments. Learners deploy OCTO APM Demo, a drone retail stack with a browser storefront, FastAPI services, a Spring Boot payment sidecar, OKE, and Oracle Autonomous Database.

The workshop teaches four practical use cases. Learners monitor OKE with the Log Analytics Kubernetes Monitoring Solution, inspect the Log Analytics Security Monitoring Solution, follow a distributed transaction in OCI APM, and diagnose a database-bound bottleneck with APM, Ops Insights, and Database Management.

The final lab turns the evidence into an operating model. Learners validate a Monitoring alarm, route an OCI resource event through Events and Notifications, and query Resource Analytics for OCTO inventory and relationship context.

## Focused Services

- OCI Monitoring
- OCI Log Analytics
- OCI Events
- OCI Application Performance Monitoring
- OCI Database Management
- OCI Ops Insights
- OCI Resource Analytics

OCI Notifications and Connector Hub are supporting services.

## Workshop Outline

1. Introduction
2. Lab 1 - OCTO APM Demo Quickstart Deployment
3. Lab 2 - Connect OCI Observability Services
4. Lab 3 - Trace a Customer Transaction End to End
5. Lab 4 - Investigate Application and Database Incidents
6. Lab 5 - Operationalize Monitoring, Events, and Resource Analytics

## Workshop Prerequisites

- An OCI tenancy and compartment for the OCTO resources.
- An OKE deployment for the complete workshop path.
- Permission to use the focused services and supporting Notifications topic.
- Administrator-assisted onboarding for the Log Analytics Kubernetes and Security solutions.
- A pre-provisioned Resource Analytics instance with populated data and database access.
- A configured OCTO checkout from `https://github.com/adibirzu/octo-observability-demo`.
- Access to `https://drones.${DNS_DOMAIN}` and `https://admin.${DNS_DOMAIN}`.

## Notes

- Mode: `publish-ready`.
- Target duration: 6.5 hours across exactly five labs.
- OCTO APM Demo is the source of truth for commands, endpoints, service names, and telemetry fields.
- Resource Analytics SQL runs against the Resource Analytics Autonomous AI Database. FreeSQL is not suitable for tenancy-specific inventory data.
- The workshop uses console checkpoints and text evidence because local publishable screenshots are not available.

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
