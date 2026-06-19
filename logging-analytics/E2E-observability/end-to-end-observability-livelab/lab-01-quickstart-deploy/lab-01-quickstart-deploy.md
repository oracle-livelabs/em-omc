# Lab 1: QuickStart Deployment

## Introduction

In this lab, you deploy the OCI-DEMO foundation, application platform, control plane, Enterprise CRM Portal, and OCTO Drone Shop. This gives the rest of the workshop a live application path that can generate traces, logs, metrics, WAF events, database activity, and agent telemetry.

Estimated Time: 70 minutes

### Objectives

In this lab, you will:

- Configure the OCI-DEMO deployment environment.
- Run the Quick Start dry-run and deployment commands.
- Deploy the control plane and the e-commerce application workloads.
- Verify the control plane, CRM, and Drone Shop endpoints.
- Confirm the runtime and deployment services that make the workshop portable.

## Task 1: Configure the Deployment Environment

1. Open a terminal on the workstation, bastion, or Cloud Shell session that will run the OCI-DEMO deployment.

2. Clone the OCI-DEMO repository or switch to your existing checkout.

    ```bash
    git clone https://github.com/adibirzu/OCI-DEMO.git
    cd OCI-DEMO
    ```

3. Create the local environment file.

    ```bash
    cp .env.example .env.local
    ```

4. Edit `.env.local` with the values for your tenancy, compartment, region, OCI authentication mode, DNS settings, APM domain values, and application hostnames.

5. Confirm that OCI authentication works from the deployment host.

    ```bash
    oci iam region list --output table
    ```

6. If you are using a non-default OCI CLI profile or an instance principal, record the exact mode because you will reuse it in later commands.

    ```bash
    # Profile example
    python3 deploy.py --component c2 --oci-profile <your-profile> --oci-tenancy <tenancy-ocid> --dry-run

    # Instance principal example
    python3 deploy.py --component c2 --oci-auth-mode instance_principal --dry-run
    ```

## Task 2: Run the Quick Start Deployment

1. Run a full dry-run first. The deployment engine resolves the dependency graph, skips already deployed prerequisites, and previews the plan.

    ```bash
    python3 deploy.py --component all --dry-run
    ```

2. Review the plan output. Confirm that the plan includes the foundation, observability, OKE, control plane, Enterprise CRM Portal, OCTO Drone Shop, GenAI, Agent Fabric, and Langfuse components needed for this workshop.

3. Deploy the full environment when you are ready.

    ```bash
    python3 deploy.py --component all
    ```

4. If your instructor asks you to deploy only the workshop path, deploy the required component groups instead of `all`.

    ```bash
    python3 deploy.py --component c0,c1,c2,c8,c11,c11b,c15,c27,c28,c12,c24,c34
    ```

5. If your tenancy has a temporary service-limit preflight issue and your instructor approves the exception, rerun the specific component with the skip flag.

    ```bash
    python3 deploy.py --component c7 --skip-limits-check
    ```

## Task 3: Deploy and Open the Control Plane

1. Run the control-plane setup script when your Quick Start run requires the direct control-plane setup path.

    ```bash
    bash control_plane/setup_control_plane.sh
    ```

2. Verify the Control Plane VM component.

    ```bash
    python3 deploy.py --verify c11
    ```

3. Verify the OKE-hosted control plane.

    ```bash
    python3 deploy.py --verify c11b
    ```

4. Open the canonical public control-plane URL.

    ```text
    https://cp.octodemo.cloud
    ```

5. In the control plane, confirm that the navigation includes observability pages such as DB Management, Ops Insights, Monitoring, Stress Test, Drone Shop, and GenAI Observability.

## Task 4: Verify the Application Workloads

1. Verify the Enterprise CRM Portal.

    ```bash
    python3 deploy.py --verify c27
    ```

2. Verify the OCTO Drone Shop.

    ```bash
    python3 deploy.py --verify c28
    ```

3. Check the public health endpoints.

    ```bash
    curl -I https://crm.octodemo.cloud/health
    curl -I https://shop.octodemo.cloud/health
    curl -I https://shop.octodemo.cloud/api/integrations/crm/health
    ```

4. Check deployment status.

    ```bash
    python3 deploy.py --status
    ```

5. Record these values for later labs:

    - Control plane URL
    - CRM Portal URL
    - Drone Shop URL
    - APM domain name and OCID
    - Log Analytics namespace
    - OKE cluster name
    - Autonomous Database name

## Task 5: Confirm the Portable Runtime Contract

1. In the OCI Console, confirm which runtime your deployment uses for the application path.

    - Compute VM running containers.
    - Managed Kubernetes cluster through OKE.
    - Both runtimes when your demo environment includes both.

2. Confirm that OCI Resource Manager, Terraform, or the deployment engine created the runtime and observability resources together.

3. Confirm that the deployment includes supporting services when your environment enables them:

    - OCIR for container images.
    - Vault or KMS for secrets and wallet material.
    - Service Connector Hub for OCI Logging to Log Analytics routing.
    - Notifications for alarm delivery.
    - Load Balancer and WAF for public edge traffic.

4. Record the runtime value that should appear on spans or resource attributes.

    ```text
    app.runtime = oke | compute | local
    service.namespace = octo
    db.target = octo-atp
    ```

5. Keep these values for later labs. They prove that the same correlation contract works even when the app moves between Compute and OKE.

## Learn More

- [OCI-DEMO Quick Start](https://github.com/adibirzu/OCI-DEMO#quick-start)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 18, 2026
