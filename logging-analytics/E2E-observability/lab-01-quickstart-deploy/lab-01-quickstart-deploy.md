# Lab 1: OCTO APM Demo Quickstart Deployment

## Introduction

In this lab, you deploy OCTO APM Demo from `adibirzu/octo-observability-demo`. The platform gives the rest of the workshop a live drone retail path that produces browser telemetry, FastAPI spans, Spring Boot payment spans, structured logs, custom metrics, Kubernetes state, and Oracle Database activity.

Estimated Time: 70 minutes

### Objectives

In this lab, you will:

- Clone the OCTO APM Demo repository.
- Configure the `env.template` deployment values.
- Deploy the OKE reference path with Resource Manager, `make`, or Helm.
- Verify the OCTO Drone Shop and Enterprise CRM Portal endpoints.
- Confirm the runtime and correlation fields used by later labs.

## Task 1: Configure the Deployment Environment

1. Open a terminal on the workstation, bastion, or Cloud Shell session that will run the deployment.

2. Clone the OCTO APM Demo repository or switch to your existing checkout.

    ```bash
    git clone https://github.com/adibirzu/octo-observability-demo.git
    cd octo-observability-demo
    ```

3. Create the deployment environment file.

    ```bash
    cp env.template .env
    ```

4. Edit `.env` with your tenancy values.

    ```text
    OCI_PROFILE=DEFAULT
    OCI_COMPARTMENT_ID=<compartment-ocid>
    OCIR_REGION=<oci-region>
    OCIR_TENANCY=<object-storage-namespace>
    DNS_DOMAIN=<your-dns-zone>
    ```

5. Confirm that OCI authentication works from the deployment host.

    ```bash
    oci iam region list --profile "${OCI_PROFILE:-DEFAULT}" --output table
    ```

6. Run the platform preflight check.

    ```bash
    make doctor
    ```

7. Fix any failed preflight item before you deploy. The quickstart expects working `oci`, `jq`, `curl`, `bash`, and the tools required by your chosen deployment path.

## Task 2: Choose a Deployment Path

1. Use the **OKE Resource Manager stack** for the complete workshop. Labs 2 and 4 require a Kubernetes cluster that Log Analytics can monitor.

    ```text
    https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/adibirzu/octo-observability-demo/releases/download/resource-manager-stack/octo-stack.zip
    ```

2. In OCI Resource Manager, provide the target compartment, DNS domain, and resource prefix. Confirm that the stack includes OKE, ATP, APM, Logging, Log Analytics, and Monitoring resources.

3. Run **Plan** and then **Apply**.

4. Use the `make` quickstart when you want to inspect and customize the OKE deployment.

    ```bash
    make tenancy-init
    make deploy
    ```

5. Use per-service targets only when you need to update one workload.

    ```bash
    make deploy-shop
    make deploy-crm
    make deploy-java-apm
    ```

6. Use the Helm chart when your workshop environment standardizes on Helm.

    ```bash
    make deploy-helm
    ```

7. The private Compute stack remains a supported OCTO deployment, but it cannot complete the OKE-specific exercises without a separate Kubernetes target.

8. Use the local stack only for code exploration. Local mode does not send signals to OCI APM, Log Analytics, or OCI Monitoring.

    ```bash
    make local-up
    ```

## Task 3: Point DNS and Smoke Test

1. After deployment, record the public load balancer IP addresses from the Resource Manager output or `make deploy` output.

2. Create DNS A records for the two application hostnames.

    ```text
    drones.${DNS_DOMAIN}    A    <shop-lb-ip>
    admin.${DNS_DOMAIN}     A    <crm-lb-ip>
    ```

3. Wait for DNS propagation.

4. Run the platform smoke test.

    ```bash
    make smoke
    ```

5. If you used Resource Manager and do not have the repo shell available, run the deployment validator directly.

    ```bash
    DNS_DOMAIN=<your-dns-zone> ./deploy/validate-deployment.sh
    ```

6. Confirm that the smoke test reports the storefront, admin portal, APM, OCI Logging, workflow gateway, and Java sidecar checks as healthy. Treat optional module checks separately.

## Task 4: Verify the Application Workloads

1. Open the OCTO Drone Shop.

    ```text
    https://drones.${DNS_DOMAIN}
    ```

2. Open the Enterprise CRM Portal.

    ```text
    https://admin.${DNS_DOMAIN}
    ```

3. Check the readiness endpoints.

    ```bash
    curl -sS https://drones.${DNS_DOMAIN}/ready | jq
    curl -sS https://admin.${DNS_DOMAIN}/ready | jq
    ```

4. Confirm that the readiness response includes the OCI observability fields.

    ```json
    {
      "ready": true,
      "database": "connected",
      "apm_configured": true,
      "rum_configured": true,
      "logging_configured": true,
      "java_apm_enabled": true
    }
    ```

5. If the OKE deployment path is active, verify the Kubernetes workloads.

    ```bash
    kubectl get deploy -n octo-drone-shop
    kubectl get deploy -n enterprise-crm
    kubectl rollout status deployment/octo-drone-shop -n octo-drone-shop
    kubectl rollout status deployment/enterprise-crm-portal -n enterprise-crm
    ```

6. Record these values for later labs:

    - Drone Shop URL.
    - Enterprise CRM Portal URL.
    - DNS domain.
    - APM domain name and OCID.
    - Log Analytics namespace.
    - OKE cluster name and OCID.
    - Autonomous Database name.
    - Resource Manager stack name and OCID.

## Task 5: Confirm the Portable Runtime Contract

1. Confirm which runtime your deployment uses for the application path.

    - OKE through Resource Manager, raw manifests, or Helm.
    - Private Compute as an optional portability path.
    - Local stack for code-only exploration.

2. Confirm that the deployment includes supporting OCI resources when your environment enables them.

    - OCIR repositories for container images.
    - OCI APM domain and data keys.
    - OCI Logging log group.
    - Service Connector Hub connectors into Log Analytics.
    - OCI Monitoring custom metrics and alarms.
    - Load Balancer and WAF for public edge traffic.
    - OCI Notifications topic for alarms and Events actions.

3. Record the runtime values that should appear on spans, logs, or metrics.

    ```text
    service.namespace = octo
    service.name = octo-drone-shop | enterprise-crm-portal | octo-apm-java-demo
    deployment.environment = production | staging | dev
    app.runtime = oke | compute | local
    db.target = octo-atp
    ```

4. Record the primary correlation fields that later labs use.

    ```text
    trace_id:
    span_id:
    oracleApmTraceId:
    oracleApmSpanId:
    request_id:
    workflow_id:
    ```

5. Keep these values for later labs. They connect browser, application, Java sidecar, Kubernetes, logs, metrics, events, and ATP evidence.

## Learn More

- [OCTO APM Demo repository](https://github.com/adibirzu/octo-observability-demo)
- [OCTO APM Demo Quickstart](https://github.com/adibirzu/octo-observability-demo/blob/main/docs/QUICKSTART.md)
- [OCTO APM Demo OKE deployment](https://github.com/adibirzu/octo-observability-demo/blob/main/deploy/oke/README.md)
- [OCTO APM Demo correlation contract](https://github.com/adibirzu/octo-observability-demo/blob/main/site/architecture/correlation-contract.md)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, July 1, 2026
