# CloudBees Unify Candidate Demo — Component (CI + Deploy)

A lightweight starter kit for SE candidates building a CloudBees Unify demo as part of an interview. This is the **Component** repository: continuous integration (build/test/scan) and component deployment for the `orders-api` component.

> **Release Orchestration lives in a separate repo.** In CloudBees Unify an Application and a Component cannot be the same repository, so the staged, governed **release workflows** are in the Application repo:
> **[cb-demos/cloudbees-unify-demo-app](https://github.com/cb-demos/cloudbees-unify-demo-app)**

**This is a simulated application delivery demo.** CloudBees runs the orchestration, publishes recorded test results and evidence, and registers artifact metadata. No cluster, registry, or third-party service credentials are required. Connect the repository to Unify and verify a run in your organization before presenting.

The JUnit fixture intentionally includes **14 passed tests, one failed test, and one skipped test**. This workflow does not execute application tests or a security scanner, and it does not build a container image. A green workflow is not proof of passing application quality checks. Inspect actual security findings separately in the component Security tab.

## Quick start

1. **Fork** this repository.
2. **Connect** the fork to your CloudBees Unify organization as a **Component**.
3. Open a workflow under `.cloudbees/workflows/` and click **Run workflow** — they succeed on their own with mock output.
4. For the end-to-end release story, also connect the [application repo](https://github.com/cb-demos/cloudbees-unify-demo-app) and run one of its release workflows.

## What is included

Workflows (runnable standalone via **Run workflow**):

- `.cloudbees/workflows/ci.yaml` — CI: validate → unit tests → security scan → package. The package job **registers a build artifact** (`orders-api` version `1.4.<run>`) with CloudBees Unify so releases have an artifact to deploy. Each job publishes evidence to the run's Evidence tab.
- `.cloudbees/workflows/deploy.yaml` — simulated component deploy (callable by the application's deployer via `workflow_call`, or run standalone). Mock/echo only — no real cluster — and publishes evidence.
- `.github/workflows/ci.yml` — GitHub Actions CI alternative, to show external-toolchain integration

Supporting assets:

- `k8s/` — Kubernetes manifests for a simple demo app
- `helm/unify-demo-app/` — basic Helm chart for deployment storytelling

## Suggested demo path

1. Show the repo structure — teams keep their existing tools; Unify orchestrates.
2. Run `ci.yaml` to show a standardized build/test/security pipeline, then walk its **Evidence** tab.
3. Run `deploy.yaml` to show component deployment.
4. Switch to the **[application repo](https://github.com/cb-demos/cloudbees-unify-demo-app)** and run a staged release workflow (FinSure Bank or Horizon Health) to tell the end-to-end governance/release story with per-job evidence.
5. Close on business outcomes: visibility, governance, orchestration, developer productivity, and preserving existing tool investments.

## Customizing

These are intentionally simple building blocks. To make the demo yours:

- Rename the application/components to fit your scenario (e.g. `Customer Portal` / `orders-api`).
- Add or remove a tool integration to match the customer's toolchain.
- Pair with the application repo to show the full **build → release** story across a Component and an Application.
