# Lab 5: Monitor Agent Behavior and Detect Anomalies

## Introduction

In this lab, you monitor the AI agent path in OCI-DEMO. You will verify the GenAI, Agent Fabric, and Langfuse components, generate baseline agent activity, introduce a controlled behavior change, and detect the change from traces, logs, metrics, token usage, tool execution, and anomaly indicators.

Estimated Time: 75 minutes

### Objectives

In this lab, you will:

- Deploy and verify the GenAI and Agent Fabric components used by agent monitoring.
- Capture agent, tool, retrieval, and model spans in OCI APM.
- Correlate OCI APM traces with Langfuse or LLM observability evidence.
- Identify behavior changes, judge-score changes, and anomaly signals from agent execution patterns.
- Use OCI Generative AI Agents concepts for agent endpoints, tools, and runtime validation.

## Task 1: Verify the Agent Monitoring Components

1. From the OCI-DEMO repository, deploy or verify the GenAI component.

    ```bash
    python3 deploy.py --component c12
    python3 deploy.py --verify c12
    ```

2. Deploy or verify Agent Fabric.

    ```bash
    python3 deploy.py --component c24
    python3 deploy.py --verify c24
    ```

3. Deploy or verify Langfuse LLM Observability when it is part of your environment.

    ```bash
    python3 deploy.py --component c34
    python3 deploy.py --verify c34
    ```

4. Confirm that `.env.local` or the component state includes the required APM values.

    ```text
    C12_OTEL_ENABLED=true
    OCI_APM_ENDPOINT=<apm-otlp-endpoint>
    OCI_APM_PRIVATE_DATAKEY=<private-data-key>
    OCI_APM_DOMAIN_ID=<apm-domain-ocid>
    OCI_APM_REGION=<region>
    C24_ENABLED=true
    ```

5. Open the GenAI Observability page.

    ```text
    https://cp.octodemo.cloud/genai-observability
    ```

6. Confirm that the page shows GenAI status, trace summaries, token metrics, conversations, RAG activity, and Agent Fabric or MCP tool metrics when your deployment enables those modules.

7. Map the runtime to OCI Generative AI Agents concepts.

    | Agent concept | Evidence to find |
    | --- | --- |
    | Agent | configured coordinator or operations agent. |
    | Tool | RAG, SQL, function calling, MCP, or operations tool. |
    | Endpoint | runtime endpoint or control-plane route used for chat. |
    | Session | conversation ID, trace ID, or request ID. |
    | Guardrail | denied action, approval requirement, or policy event. |

8. If your environment uses the Agent Development Kit, record the ADK package, application entry point, and deployment target.

## Task 2: Generate Baseline Agent Activity

1. Open the control-plane GenAI or agent interface.

2. Submit a simple operational prompt that should use a small number of tools.

    ```text
    Summarize the health of the Drone Shop and identify any recent errors in the last 15 minutes.
    ```

3. Submit a database-oriented prompt.

    ```text
    Check whether the Autonomous Database shows unusual waits or slow SQL for the Drone Shop checkout flow.
    ```

4. Submit an observability-oriented prompt.

    ```text
    Find recent Log Analytics records for the latest Drone Shop trace and explain the likely user impact.
    ```

5. Record the prompt timestamp, conversation ID if shown, selected model, and visible answer path.

6. Wait one to three minutes for trace and log data to arrive in OCI APM and Log Analytics.

7. For each prompt, record whether the answer used:

    - model-only response.
    - RAG retrieval.
    - SQL tool.
    - function calling.
    - MCP or operations tool.
    - guardrailed action requiring approval.

## Task 3: Inspect Agent Traces in OCI APM

1. Open OCI APM Trace Explorer for the APM domain.

2. Filter to the last 15 minutes.

3. Search for GenAI or agent spans. Use the attributes that exist in your environment.

    ```text
    gen_ai.operation.name
    gen_ai.request.model
    gen_ai.usage.input_tokens
    gen_ai.usage.output_tokens
    gen_ai.tool.name
    ```

4. Open a trace from one of your prompts.

5. Confirm that the trace hierarchy shows the user request, agent planning or routing, tool execution, retrieval or database work, and model call when your deployment enables those stages.

6. Record these baseline values:

    - total duration.
    - tool count.
    - failed tool count.
    - input token count.
    - output token count.
    - model name.
    - agent mode.

7. Inspect semantic attributes on the span. Use the attributes present in your environment.

    ```text
    gen_ai.operation.name:
    gen_ai.request.model:
    gen_ai.response.model:
    gen_ai.usage.input_tokens:
    gen_ai.usage.output_tokens:
    gen_ai.tool.name:
    error.type:
    ```

8. Record whether the trace shows planning, retrieval, tool execution, model call, and response formatting as separate spans.

## Task 4: Correlate with Langfuse and Logs

1. Open the Langfuse or LLM observability UI for the deployment if your environment includes C34.

2. Search for the same prompt timestamp, trace ID, conversation ID, or model name.

3. Confirm that Langfuse shows an AI-native trace hierarchy such as user, agent, tool, and LLM call.

4. Compare Langfuse duration, token, model, tool metadata, and judge or evaluation score with the OCI APM trace when those fields exist.

5. Open Log Analytics and search for the same trace ID, conversation ID, or agent service name.

    ```text
    '<trace-id>' or '<conversation-id>'
    ```

6. Record the common join key that worked best in your environment.

7. Record whether the agent answer shows an evaluation or LLM-as-judge score. If it does, capture the score and the trace ID beside it.

8. Compare the same run across the available observability stores.

    | Store | Evidence |
    | --- | --- |
    | OCI APM | trace hierarchy, duration, errors, span attributes. |
    | Log Analytics | warnings, denied actions, tool errors, trace ID logs. |
    | Monitoring | token, request, latency, or error metrics. |
    | Langfuse | LLM trace hierarchy, model, tokens, cost, quality scores. |
    | Control Plane | conversation ID, model route, agent mode, tool summary. |

## Task 5: Detect a Controlled Behavior Change

1. Generate a prompt that should increase tool usage or latency without changing production data.

    ```text
    Compare Drone Shop health, CRM integration health, database waits, recent WAF events, and recent Log Analytics errors. Return the evidence for each source.
    ```

2. Generate a prompt that should trigger a guardrail, denied tool, invalid target, or handled error. Use a safe prompt that your instructor approves for your tenancy.

    ```text
    Attempt to run a write operation without approval and explain why it requires confirmation first.
    ```

3. In APM, compare the controlled behavior-change traces with your baseline traces.

4. Look for anomaly indicators such as:

    - higher p95 duration.
    - increased tool count.
    - new tool names.
    - failed or denied tool calls.
    - model route change.
    - token count spike.
    - judge-score or quality-score drop.
    - repeated retrieval misses.
    - guardrail or policy events.

5. In Log Analytics, search for agent warnings, denied actions, or tool errors around the same time.

    ```text
    Message contains 'agent' and (Message contains 'denied' or Message contains 'guardrail' or Message contains 'tool' or Message contains 'error')
    ```

6. In OCI Monitoring or the GenAI Observability dashboard, compare the latest point against the previous baseline for latency, errors, requests, and token usage.

7. Draft Monitoring and Log Analytics detection logic for the agent anomaly. Do not create alarms unless your instructor asks you to.

    ```text
    Signal:
    Baseline:
    Threshold:
    Window:
    Owner:
    Notification target:
    ```

8. Write the anomaly finding.

    ```text
    Baseline behavior:
    Changed behavior:
    First signal that changed:
    Confirming APM evidence:
    Confirming Log Analytics evidence:
    Confirming Langfuse or token evidence:
    Likely cause:
    Recommended next action:
    ```

9. Confirm that traces, logs, and metrics captured the behavior change without requiring a production incident.

## Learn More

- [OCI Generative AI Agents](https://docs.oracle.com/en-us/iaas/Content/generative-ai-agents/home.htm)
- [OCI Application Performance Monitoring](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/)
- [Configure OpenTelemetry and other tracers for OCI APM](https://docs.oracle.com/en-us/iaas/application-performance-monitoring/doc/configure-open-source-tracing-systems.html)
- [OCI Log Analytics](https://docs.oracle.com/en-us/iaas/log-analytics/)
- [OCI Monitoring](https://docs.oracle.com/en-us/iaas/Content/Monitoring/home.htm)
- [OCI Service Connector Hub](https://docs.oracle.com/en-us/iaas/Content/connector-hub/home.htm)

## Acknowledgements

* **Authors** - Alexandru Birzu, Observability and Manageability Black Belt; Royce Fu, Master Principal Cloud Architect
* **Last Updated By/Date** - Royce Fu, June 18, 2026
